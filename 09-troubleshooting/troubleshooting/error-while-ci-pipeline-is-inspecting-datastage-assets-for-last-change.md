# Error while CI pipeline is 'Inspecting DataStage assets for last change'

# Problem

```
Attempting to identify last change with 8 working threads.
Inspecting DataStage assets for last change...
* Check demo1-engn.datamigrators.io/wwi_jenkins_ds115_dev/Jobs/ParameterSets/pGlobal.pst - FAILED
      3 retries attempted before failure
      Dec 08, 2020 12:19:25 PM com.ibm.xmeta.binding.impl.RemoteSandboxBinding invokeOperation
      SEVERE: Caught RemoteException: enum constant ASSET_IMPORT_NOTIFICATION does not exist in class com.ibm.xmeta.util.config.FeatureToggleConstants; nested exception is: 
      	java.io.InvalidObjectException: enum constant ASSET_IMPORT_NOTIFICATION does not exist in class com.ibm.xmeta.util.config.FeatureToggleConstants
      java.rmi.RemoteException: enum constant ASSET_IMPORT_NOTIFICATION does not exist in class com.ibm.xmeta.util.config.FeatureToggleConstants; nested exception is: 
      	java.io.InvalidObjectException: enum constant ASSET_IMPORT_NOTIFICATION does not exist in class com.ibm.xmeta.util.config.FeatureToggleConstants
```

# Cause

This is usually an indication that istool and DataStage versions are not aligned (i.e. there is a difference in XMeta patch levels). 

# Solution

Double check the size/versions across services, engine and client:

*   [**Installing a new IBM InfoSphere Information Server 11.5.0.2 Engine tier fails if the Services tier is already at 11.5.0.2 Service Pack 2 level**](https://www.ibm.com/support/pages/installing-new-ibm-infosphere-information-server-11502-engine-tier-fails-if-services-tier-already-11502-service-pack-2-level) - Information Server 11.5.0.2 Engine tier installation fails with the following error if the Services tier is already at Information Server 11.5.0.2 Service Pack 2 level. `Caught RemoteException: enum constant ASSET_IMPORT_NOTIFICATION does not exist in class com.ibm.xmeta.util.config.FeatureToggleConstants`
    

*   [**JR58925: UNABLE TO ADD A NEW ENGINE NODE WHEN RUNNING IS 11.5.0.2 SP2**](https://www.ibm.com/support/pages/apar/JR58925) - Unable to add a new Engine node when running IS 11.5.0.2 SP2, the installer fails while creating new Project on the new node