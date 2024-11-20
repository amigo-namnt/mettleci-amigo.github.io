# JWT rejected due to invalid signature

# Symptom

After restarting the MettleCI Workbench service, `mci.log` will have entries similar to the below, containing `JWT rejected due to invalid signature` and a signature string:

```
10.107.146.223 - - [25/Mar/2022:12:49:42 +0000] "GET /api/notification HTTP/1.1" 101 0 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36" 39
WARN  [2022-03-25 12:49:46,667] com.github.toastshaman.dropwizard.auth.jwt.JwtAuthFilter: Error decoding credentials: JWT rejected due to invalid signature. Additional details: [[9] Invalid JWS Signature: JsonWebSignature{"alg":"HS256"}->eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIzIiwidXNlcm5hbWUiOiJsZGVsdmVhdXgiLCJyb2xlcyI6WyJERVZFTE9QRVIiXSwiaWF0IjoxNjQ4MjEyNTU5LCJqdGkiOiJoTnl1ejFFTnVFZVBQNFpQVnhnNDhBIn0.KXmFscUFqPAJ3R3vBvnGelZMCc7Fdxk7-8LXSuPOPQg]
! org.jose4j.jwt.consumer.InvalidJwtSignatureException: JWT rejected due to invalid signature. Additional details: [[9] Invalid JWS Signature: JsonWebSignature{"alg":"HS256"}->eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIzIiwidXNlcm5hbWUiOiJsZGVsdmVhdXgiLCJyb2xlcyI6WyJERVZFTE9QRVIiXSwiaWF0IjoxNjQ4MjEyNTU5LCJqdGkiOiJoTnl1ejFFTnVFZVBQNFpQVnhnNDhBIn0.KXmFscUFqPAJ3R3vBvnGelZMCc7Fdxk7-8LXSuPOPQg]
! at org.jose4j.jwt.consumer.JwtConsumer.processContext(JwtConsumer.java:216)
! at org.jose4j.jwt.consumer.JwtConsumer.process(JwtConsumer.java:416)
! at com.github.toastshaman.dropwizard.auth.jwt.JwtAuthFilter.verifyToken(JwtAuthFilter.java:88)
! at com.github.toastshaman.dropwizard.auth.jwt.JwtAuthFilter.filter(JwtAuthFilter.java:47)
! at io.dropwizard.auth.chained.ChainedAuthFilter.filter(ChainedAuthFilter.java:45)
```

# Diagnosis

A [JWT (JSON Web Token)](https://jwt.io/introduction) is a signature-based security protocol which MettleCI Workbench uses to authorize previously authenticated users. When a user logs into MettleCI Workbench, a JWT is generated and signed with a private cryptographic key known only to the MettleCI Workbench service. All subsequent communication between the logged in user’s browser session and the MettleCI Workbench service includes the JWT which is validated to have originated from MettleCI Workbench by validating the cryptographic signature. Any JWT tokens which do not have a matching cryptographic signature are rejected.

MettleCI Workbench automatically generates a new private cryptographic key every time it is started. This ensures private cryptographic keys are never stored and JWTs are impossible to forge. As a consequence of this design, restarting the MettleCI Workbench Server will invalidate all previously generated JWTs. Previously logged in browser sessions will continue to use the existing JWTs which will be rejected by the server because they are now invalid. When this occurs, the described warning message will be logged to `mci.log` and the user will be prompted to log in again.

# Solution

This warning message is logged to record that an invalid JWT token was rejected, it is a normal part of operation after restarting MettleCI Workbench with previously logged in users and can be safely ignored. Future versions of MettleCI Workbench may suppress this warning by default.