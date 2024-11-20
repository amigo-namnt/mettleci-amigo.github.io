# Integrating Atlassian Jira with MettleCI Workbench

*   [Introduction](#introduction)
    *   [Certificate filename extensions](#certificate-filename-extensions)
*   [Step 1 - Generating an RSA Public/Private Key Pair](#step-1-generating-an-rsa-publicprivate-key-pair)
    *   [Process Overview](#process-overview)
    *   [Steps](#steps)
*   [Step 2 - Creating a Jira Application Link](#step-2-creating-a-jira-application-link)
*   [Step 3 - Enter the credentials into workbench](#step-3-enter-the-credentials-into-workbench)
*   [Step 4 - Testing your connection](#step-4-testing-your-connection)

> [!INFO]
> Note that this page describes how MettleCI can authenticate against Atlassian Jira using OAuth. Atlassian’s documentation on OAuth is available [here](https://developer.atlassian.com/cloud/jira/platform/jira-rest-api-oauth-authentication/).

# Introduction

In cryptography, [X.509](https://en.wikipedia.org/wiki/X.509) is widely-adopted standard defining the format of public key certificates. X.509 certificates are used in many Internet protocols, including TLS/SSL which is the basis for HTTPS. An X.509 certificate binds an identity to a public key using a digital signature. A certificate contains an identity (a hostname, or an organization, or an individual) and a public key (using an encryption scheme such as RSA, DSA, ECDSA, etc.), and is either signed by a certificate authority or is self-signed. When a certificate is signed by a trusted certificate authority, or validated by other means, someone holding that certificate can use the public key it contains to establish secure communications with another party. In this case the certificate will be used to provide a secure communication mechanism between Atlassian Jira and MettleCI Workbench.

### Certificate filename extensions

There are several commonly used filename extensions for X.509 certificates. These are the ones which will feature in the process described here:

*   `.pem` – ([Privacy-enhanced Electronic Mail](https://en.wikipedia.org/wiki/Privacy-enhanced_Electronic_Mail)) is a [Base64](https://en.wikipedia.org/wiki/Base64) encoded [DER](https://en.wikipedia.org/wiki/Distinguished_Encoding_Rules) certificate enclosed between `-----BEGIN CERTIFICATE-----` header and `-----END CERTIFICATE-----` footer.
    
*   `.cer` – this certificate file stores information about one X.509 owner certificate and a specific public key.
    
*   `.pkcs8` – Public-Key Cryptography Standards [(PKCS) #8](https://en.wikipedia.org/wiki/PKCS_8) is a standard syntax for storing private key information created by RSA Laboratories. The PKCS #8 private key may be encrypted with a passphrase and typically exchanges keys in the [PEM](https://en.wikipedia.org/wiki/Privacy-enhanced_Electronic_Mail) [base64](https://en.wikipedia.org/wiki/Base64)\-encoded format which uses values enclosed between `-----BEGIN PRIVATE KEY-----` header and `-----END PRIVATE KEY-----` footer (or `-----BEGIN ENCRYPTED PRIVATE KEY-----` and `-----END ENCRYPTED PRIVATE KEY-----` if you use a passphrase.)
    

# Step 1 - Generating an RSA Public/Private Key Pair

## Process Overview

![](./attachments/Creating%20Jira%20Keypair.png)

If you haven’t already, you will need to either:

*   Create a key pair for Workbench to use to authenticate with Jira, or
    
*   Request a `.pem` file from your Jira administrator for MettleCI Workbench to use for Jira integration.
    

> [!WARNING]
> Note that a common error is to misspell [**pkcs**](https://en.wikipedia.org/wiki/PKCS_8) as 'pcks'. Please check your spelling is correct when following the instructions below.

## Steps

On any secure machine with `openssl` installed (It is easiest doing this directly on your DataStage Engine where MettleCI Workbench is installed)…

1.  Generate a 1024-bit private key: `jira_privatekey.pem`
    
    ```
    $> openssl genrsa -out jira_privatekey.pem 1024
    Generating RSA private key, 1024 bit long modulus
    .......++++++
    ..++++++
    e is 65537 (0x10001)
    $>
    ```
    
2.  Create an X509 certificate: `jira_publickey.cer`
    
    ```
    $> openssl req -newkey rsa:1024 -x509 -key jira_privatekey.pem -out jira_publickey.cer -days 3650
    You are about to be asked to enter information that will be incorporated
    into your certificate request.
    What you are about to enter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', the field will be left blank.
    -----
    Country Name (2 letter code) [XX]:AU
    State or Province Name (full name) []:Victoria
    Locality Name (eg, city) [Default City]:Melbourne
    Organization Name (eg, company) [Default Company Ltd]:Data Migrators Pty Ltd
    Organizational Unit Name (eg, section) []:MettleCI
    Common Name (eg, your name or your server's hostname) []:myhost.datamigrators.io
    Email Address []:admin@mettleci.com
    $>
    ```
    
3.  Extract the private key (PKCS8 format) to a ‘pkcs8’ file: `jira_privatekey.pkcs8`
    
    ```
    $> openssl pkcs8 -topk8 -nocrypt -in jira_privatekey.pem -out jira_privatekey.pkcs8
    $> ll jira_*
    -rw-r--r-- 1 mciworkb dstage  916 Aug  2 15:10 jira_privatekey.pkcs8
    -rw-r--r-- 1 mciworkb dstage  887 Aug  2 15:05 jira_privatekey.pem
    -rw-r--r-- 1 mciworkb dstage 1224 Aug  2 15:08 jira_publickey.cer
    $>
    ```
    
4.  Extract the public key from the certificate to a ‘pem’ file: `jira_publickey.pem` file:
    
    ```
    $> openssl x509 -pubkey -noout -in jira_publickey.cer > jira_publickey.pem
    $>
    ```
    
5.  Ensure all files are owned by the account used to execute the MettleCI Workbench service:
    
    ```
    $> chown mciworkb jira_*
    $>
    ```
    

# Step 2 - Creating a Jira Application Link

These steps are geared specifically towards Workbench. Atlassian’s own documentation is under the **Create an application link** section of this page: [https://developer.atlassian.com/server/jira/platform/oauth/](https://developer.atlassian.com/server/jira/platform/oauth/)

1.  Start by going to the **Application links** option (under **Integrations**) of your Jira Administration area.
    
    ![](./attachments/image-20201106-044950.png)
    
2.  In the field at the top (under **Configure Application Links**) enter your MettleCI Workbench URL including protocol and port number (e.g. `https://my-engine.company-intranet.com:8443`) and click **Create new link**
    
3.  On the Configure Application URL window you can leave the default **New URL** as proposed by Jira (usually identical to the **Entered URL**). **You can safely ignore the ‘No response was received…’ message** and click **Continue**.
    
    ![](./attachments/image-20220802-081030.png)
    
4.  On the next window enter the **Application Name**
    
5.  Check the **Create incoming link** checkbox IMPORTANT!
    
6.  Note that we ***will*** enter a value for **Consumer key** later on - but not in this dialog
    
7.  Click **Continue** (ensure you leave the other fields blank)
    
    ![](./attachments/image-20220802-044738.png)
    
8.  On the next dialog enter …
    
    *   A random value for **Consumer Key** (this is just an arbitrary value to uniquely identify this Application Link),
        
    *   The **Consumer Name** (e.g. ‘MettleCI Workbench’ without quotes), and
        
    *   The **Public Key** (i.e. the **contents** of `jira_publickey.pem`) that will be used by your Workbench application.
        
        ![](./attachments/image-20220802-045037.png)
        
9.  **NOTE:** The application URL specified at the top of this dialog is the URL to be specified in the **Add Issue Management** step of the Workbench Issue Management configuration, in the **Jira URL** field.
    
10.  Click **Continue**
    

# Step 3 - Enter the credentials into workbench

To create additional issue management services first use your web browser login to the Atlassian Jira user interface:

![](./attachments/image-20211112-004334.png)

Using the same browser login to MettleCI Workbench and select **User → Issue Management**:

![](./attachments/image-20210120-030257.png)

To configure a new work item management connection click the **\[+\]** button (top right)

![](./attachments/image-20210309-114641.png)

Select the work item management type **Jira** (there are also guides for [Azure](../../../mettleci-integrations/azure-devops.md), [Gitlab](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/735936684/TO+DO+-+Enabling+GitLab+Issue+Lookup+in+Workbenc), and [ServiceNow](../../../mettleci-integrations/servicenow/integrating-servicenow-work-item-lookup-with-mettleci-workbench.md)).

> [!WARNING]
> Due to a current defect the Issue Management Type drop down box may not display the 'drop down' icon on some browsers.

> [!INFO]
> The instructions below are equally applicable to self-hosted Jira instances (**Jira Server** or **Jira Data Center**) or Atlassian-hosted Jira instances (**Jira Cloud**).

![](./attachments/image-20210309-114756.png)

You will now want to fill out all the details for your particular Jira Configuration.

|     |     |
| --- | --- |
| **Name** | This can be anything you like but is often (and is best to use if possible) the name of the Jira project you’re connecting to. |
| **Jira URL** | The **Application URL** you entered when configuring the Application Link Application in Jira<br><br>If you have already configured Jira we recommend:<br><br>*   Get your Jira Key and Jira URL from the `config.yml` of the same host (most likely in `/opt/dm/mci/config.yml`) |
| **Jira Key** | The **Consumer Key** you entered when configuring the Application Link Application in Jira. |
| **Consumer Secret** | Copy and paste the **contents** of your `jira_privatekey.pkcs8` file into this field (most likely in your DataStage Engine’s `/opt/dm/mci/jira_privatekey.pkcs8` file) |

> [!INFO]
> If you have previously configured a Jira application link then you will also find the `consumerKey` and `jiraURL` in your `config.yml` file (most likely in `/opt/dm/mci/config.yml`)

# Step 4 - Testing your connection

After you’ve set this up:

1.  Restart the Workbench service
    
2.  Log into Workbench 
    
3.  Start to perform a check-in (the Job name isn’t important) but start to enter a valid Jira ID in the work item field.
    
4.  At this point you should be prompted to permit access to Jira so click on **Allow**
    
5.  ![](./attachments/image-20211112-015755.png)
    
    After this you can actually cancel the check-in since its purpose was simply to complete the Workbench-to-Jira integration.
    

Done!