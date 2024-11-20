# CP4D Unsupported Stages

|     |     |
| --- | --- |
| **Rule name** | CP4D Unsupported Stages |
| **Parallel Job** | Yes |
| **Server Job** | Yes |
| **Job Sequence** | \-  |
| **Description** | Identifies stages that are not yet supported by IBM Cloud Pak for Data |

# Description

Based on the IBM documentation:

*   [https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=sources-connectors-projects-catalogs](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=sources-connectors-projects-catalogs)
    
*   [https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=data-datastage-stages](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=data-datastage-stages)
    
*   [https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=connectors-file-in-datastage](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=connectors-file-in-datastage)
    
*   [https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=data-qualitystage-stages](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=data-qualitystage-stages)
    
*   [https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=connectors-supported-data-sources-in-datastage](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=connectors-supported-data-sources-in-datastage)
    

Note that ALL server job stages are reported as incompatible with CP4D, as DataStage Server technology is not (nor will ever likely be) supported on that platform.

# Actions

Options

*   Redesign your job to avoid the use of the incompatible stage
    
*   Speak to your IBM representative about potential forthcoming compatibility for the stage(s) in question