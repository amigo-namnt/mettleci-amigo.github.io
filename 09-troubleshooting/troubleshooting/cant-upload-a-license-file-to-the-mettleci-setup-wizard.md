# Can't upload a license file to the MettleCI Setup Wizard

# Issue

MettleCI relies on some capabilities which are not available on [Red Hat v8.3 and above **with FIPS enabled**.](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sect-security_guide-federal_standards_and_regulations-federal_information_processing_standard#doc-wrapper)

# Diagnostics

You can confirm whether or not FIPS is enabled in your Reg Hat environment using the following command:

```
cat /proc/sys/crypto/fips_enabled
```

If `fips_enabled=1` then this is likely the cause of the problem you are seeing with MettleCI.

# Resolution

The workaround for the time being is to simply disable FIPS for execution of MettleCI Workbench:

1.  Open `start-mettleci.sh` with your editor of choice.
    
2.  Copy and paste this command into the top of of the script:
    
    ```
    JAVA_OPTS=-Dcom.redhat.fips=false
    ```
    
3.  The setup wizard should now work normally.