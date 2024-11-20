# SSLHandshakeException in Workbench after configuring issue lookup

# Problem

After configuring issue lookup to an issue management system over HTTPS (where the issue management system is using a self-signed SSL certificate), the issue lookup doesn’t work as expected on the Workbench Git Commit page, and your `mci.log` file contains errors of the following form:

```
ERROR [2021-01-04 16:10:16,547] io.dropwizard.jersey.errors.LoggingExceptionMapper: Error handling a request: fa406eacdd44b94c
! sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
! at sun.security.provider.certpath.SunCertPathBuilder.build(SunCertPathBuilder.java:141)
! at sun.security.provider.certpath.SunCertPathBuilder.engineBuild(SunCertPathBuilder.java:126)
! at java.security.cert.CertPathBuilder.build(CertPathBuilder.java:280)
! at sun.security.validator.PKIXValidator.doBuild(PKIXValidator.java:451)
! ... 110 common frames omitted
! Causing: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
! at sun.security.validator.PKIXValidator.doBuild(PKIXValidator.java:456)
! at sun.security.validator.PKIXValidator.engineValidate(PKIXValidator.java:323)
! at sun.security.validator.Validator.validate(Validator.java:271)
! at sun.security.ssl.X509TrustManagerImpl.validate(X509TrustManagerImpl.java:315)
! at sun.security.ssl.X509TrustManagerImpl.checkTrusted(X509TrustManagerImpl.java:223)
! at sun.security.ssl.X509TrustManagerImpl.checkServerTrusted(X509TrustManagerImpl.java:129)
! at sun.security.ssl.CertificateMessage$T12CertificateConsumer.checkServerCerts(CertificateMessage.java:638)
```

# Cause

When communicating with an issue management system over HTTPS, MettleCI Workbench needs to verify that the SSL Certificate used by the service has been signed by a trusted authority. Out of the box, MettleCI Workbench will trust all SSL Certificates signed by globally recognized Certificate Authorities but some services can be setup using self-signed certificates. To trust a service using a self-signed certificate, the certificate needs to be added to MettleCI Workbench’s trust store.

# Solution

To add the certificate to the trust store used by MettleCI Workbench, run the following command from the MettleCI Workbench installation directory (eg. `/opt/dm/mci`) on your DataStage development engine tier:

```
java -jar <mettle-ui-x.x-xxx.jar> trust-server -url <url to server> config.yml
```

where `X.X-XXX` is the version of MettleCI Workbench currently in use, and `<url to server>` is the URL of the issue management system.

You'll need to restart the MettleCI Workbench service for the change to take effect.