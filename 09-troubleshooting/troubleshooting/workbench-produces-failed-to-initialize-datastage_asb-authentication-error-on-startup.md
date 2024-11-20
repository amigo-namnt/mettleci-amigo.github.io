# Workbench produces 'Failed to initialize DATASTAGE_ASB authentication' error on startup

# Issue

Starting the MCI Workbench Service produces output that appears to be healthy:

```
> service dm-mettleci-workbench start

Starting MettleCI Workbench ...
MettleCI Workbench: Java Executable location /bin/java
MettleCI Workbench: Java Vendor is Red
MettleCI Workbench: Java Version is 1.8
MettleCI Workbench has been started
```

But immediately checking the status of MCI Workbench shows that it failed to start:

```
> service dm-mettleci-workbench status

/opt/dm/mci/METTLE_UI.pid dead but pidfile exists
```

and the following Exception appears in the `mci.log`:

```
java.lang.RuntimeException: Failed to initialize DATASTAGE_ASB authentication method, please verify configuration or change authentication method to DATASTAGE_COMPATIBILITY
        at com.datamigrators.mettle.modules.datastage.DatastageAsbModule.providerAsbServiceFactory(DatastageAsbModule.java:54)
        <...snip...>
Caused by: java.lang.SecurityException: The IBMJCE provider may have been tampered.
        at com.ibm.crypto.provider.PBEWithMD5AndTripleDESCipher.<init>(Unknown Source)
        <...snip...>
```

# Cause

Both the DataStage Engine and MettleCI Workbench rely on a set of cryptographically signed java libraries known as `IBMJCE`. Up until version 11.7.1.4 SP1, the `IBMJCE` libraries packaged with DataStage where signed using the SHA-1 algorithm which is considered to be crypto-graphically weak by today’s standards..

[Java OpenJDK version 1.8u362](https://mail.openjdk.org/pipermail/jdk8u-dev/2023-January/016479.html) introduced a change which [disables SHA-1 Signed Java libraries](https://bugs.openjdk.org/browse/JDK-8269039). When MettleCI Workbench is using Open JDK 1.8u362 or later and attempts to load a SHA-1 Signed version of the `IBMJCE` libraries, Java security settings block the loading of many required classes and the `IBMJCE` libraries incorrectly reports that `The IBMJCE provider may have been tampered`.

# Diagnosis

Please verify…

*   whether MettleCI Workbench is version 1.0-1636 or **earlier**; and
    
*   whether it is running on Java OpenJDK version 1.8u362 or **later**.
    

Start a terminal session and connect to the DataStage Engine where MettleCI Workbench has been installed, run the following command and verify output confirms that the jar has been `signed with a weak algorithm that is now disabled`:

```
> jarsigner -verify -certs /opt/IBM/InformationServer/jdk/jre/lib/ext/ibmjceprovider.jar

The jar will be treated as unsigned, because it is signed with a weak algorithm that is now disabled.

Re-run jarsigner with the -verbose option for more details.
```

This command assumes Java OpenJDK 1.8 is on the path and Information Server has been installed in `/opt/IBM/InformationServer`.

# Solution

MettleCI Workbench version 1.0-1637+ detects `IBMJCE` library and OpenJDK security incompatibilities and will automatically adjust its runtime security settings as needed.

If you are unable to upgrade MettleCI Workbench to version 1.0-1637 or later, apply the following manual workaround:

1.  Log into the DataStage Engine where MettleCI Workbench is installed
    
2.  Open `<OpenJDK Install Directory>/jre/lib/security/java.security` for editing
    
3.  Find the `jdk.certpath.disabledAlgorithms` property and remove the `SHA1 usage SignedJAR & denyAfter 2019-01-01` entry (including any trailing `,` character)
    
4.  Find the `jdk.jar.disabledAlgorithms` property and remove the `SHA denyAfter 2019-01-01` entry (including any trailing `,` character)
    
5.  Save and restart MettleCI Workbench.
    

> [!WARNING]
> **NOTE**  
> Unlike Workbench version 1.0-1637+, this manual workaround modifies the security settings for all Java application which use the same JVM as MettleCI.

As an example, the following `java.security` file:

```
<...SNIP...>
# Example:
#   jdk.certpath.disabledAlgorithms=MD2, DSA, RSA keySize < 2048
#
jdk.certpath.disabledAlgorithms=MD2, MD5, SHA1 jdkCA & usage TLSServer, \
    RSA keySize < 1024, DSA keySize < 1024, EC keySize < 224, \
    SHA1 usage SignedJAR & denyAfter 2019-01-01, \
    include jdk.disabled.namedCurves

<...SNIP...>
# implementation. It is not guaranteed to be examined and used by other
# implementations.
#
# See "jdk.certpath.disabledAlgorithms" for syntax descriptions.
#
jdk.jar.disabledAlgorithms=MD2, MD5, RSA keySize < 1024, \
      DSA keySize < 1024, SHA1 denyAfter 2019-01-01, \
      include jdk.disabled.namedCurves
      
<...SNIP...>
```

Should be modified to look like this:

```
<...SNIP...>
# Example:
#   jdk.certpath.disabledAlgorithms=MD2, DSA, RSA keySize < 2048
#
jdk.certpath.disabledAlgorithms=MD2, MD5, SHA1 jdkCA & usage TLSServer, \
    RSA keySize < 1024, DSA keySize < 1024, EC keySize < 224, \
    include jdk.disabled.namedCurves

<...SNIP...>
# implementation. It is not guaranteed to be examined and used by other
# implementations.
#
# See "jdk.certpath.disabledAlgorithms" for syntax descriptions.
#
jdk.jar.disabledAlgorithms=MD2, MD5, RSA keySize < 1024, \
      DSA keySize < 1024, \
      include jdk.disabled.namedCurves
      
<...SNIP...>
```