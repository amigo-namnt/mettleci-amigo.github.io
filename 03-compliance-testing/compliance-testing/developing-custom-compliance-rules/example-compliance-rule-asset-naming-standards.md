# Example Compliance Rule - Asset Naming Standards

This page summarises the default naming standards that are supplied with the library of Compliance Rules which ship with MettleCI.

> [!WARNING]
> Your organisation is NOT required to use these standards. These are simply defaults that ship with the MettleCI Compliance Library, with the intent that you adapt them to your own team's needs.

*   [Parallel Job Stages](#parallel-job-stages)
*   [Server Job Stages](#server-job-stages)
*   [Job Sequence Activities](#job-sequence-activities)
*   [Blocklist](#blocklist)

## Parallel Job Stages

```
// Data Quality ---------------------------------------------------------------
'IADataRule'                     : '^dr[A-Z0-9][A-Za-z0-9|_]*'  , // Data Rules
'ExceptionStage'                 : '^exc[A-Z0-9][A-Za-z0-9|_]*' , // Exceptions
'Investigate'                    : '^inv[A-Z0-9][A-Za-z0-9|_]*' , // Investigate
'MatchFrequency'                 : '^maf[A-Z0-9][A-Za-z0-9|_]*' , // Match Frequency
'MasterDataManagementConnectorPX': '^mdm[A-Z0-9][A-Za-z0-9|_]*' , // MDM Connector
'MNS'                            : '^mns[A-Z0-9][A-Za-z0-9|_]*' , // Multi-National Standardization (MNS)
'UnduplicateMatch'               : '^udm[A-Z0-9][A-Za-z0-9|_]*' , // One Source Match
'SQA'                            : '^sqa[A-Z0-9][A-Za-z0-9|_]*' , // Standardization Quality Assessment (SQA)
'Standardize'                    : '^std[A-Z0-9][A-Za-z0-9|_]*' , // Standardize
'Survive'                        : '^srv[A-Z0-9][A-Za-z0-9|_]*' , // Survive
'ReferenceMatch'                 : '^rfm[A-Z0-9][A-Za-z0-9|_]*' , // Two Source Match
// Database -------------------------------------------------------------------
'CassandraConnectorPX'           : '^cas[A-Z0-9][A-Za-z0-9|_]*' , // Cassandra Federation
'MetaCassandraConnectorPX'       : '^cas[A-Z0-9][A-Za-z0-9|_]*' , // Cassandra Federation
'PXClassicFederation'            : '^clf[A-Z0-9][A-Za-z0-9|_]*' , // Classic Federation
'CognosTM1ConnectorPX'           : '^tm1[A-Z0-9][A-Za-z0-9|_]*' , // Cognos TM1 Connector
'DB2ConnectorPX'                 : '^db2[A-Z0-9][A-Za-z0-9|_]*' , // DB2 Connector
'DSDB2PX'                        : '^db2[A-Z0-9][A-Za-z0-9|_]*' , // DB2 UDB API Stage has been DEPRECATED
'UDBLoadPX'                      : '^db2[A-Z0-9][A-Za-z0-9|_]*' , // DB2 UDB Load has been DEPRECATED
'PxDB2'                          : '^db2[A-Z0-9][A-Za-z0-9|_]*' , // DB2/UDB Enterprise
'PxDB2Z'                         : '^db2[A-Z0-9][A-Za-z0-9|_]*' , // DB2Z has been DEPRECATED
'DTStagePX'                      : '^dts[A-Z0-9][A-Za-z0-9|_]*' , // Distributed Transaction
'DRSConnectorPX'                 : '^drs[A-Z0-9][A-Za-z0-9|_]*' , // DRS Connector
'DRSPX'                          : '^drs[A-Z0-9][A-Za-z0-9|_]*' , // Dynamic RDBMS has been DEPRECATED
'GreenplumConnectorPX'           : '^gp[A-Z0-9][A-Za-z0-9|_]*'  , // GreenPlum Connector
'HiveConnectorPX'                : '^hive[A-Z0-9][A-Za-z0-9|_]*', // Hive Connector
'InfmxCLIPX'                     : '^ifx[A-Z0-9][A-Za-z0-9|_]*' , // Informix CLI
'PxInformixXPS'                  : '^ifx[A-Z0-9][A-Za-z0-9|_]*' , // Informix Enterprise
'INFBLK10PX'                     : '^ifx[A-Z0-9][A-Za-z0-9|_]*' , // Informix Load
'XPSLoadPX'                      : '^ifx[A-Z0-9][A-Za-z0-9|_]*' , // Informix XPS Load
'Pxiway'                         : '^iway[A-Z0-9][A-Za-z0-9|_]*', // iWay Enterprise
'JDBCConnectorPX'                : '^jdbc[A-Z0-9][A-Za-z0-9|_]*', // JDBC Connector
'NetezzaConnectorPX'             : '^net[A-Z0-9][A-Za-z0-9|_]*' , // Netezza Connector
'PxNetezza'                      : '^net[A-Z0-9][A-Za-z0-9|_]*' , // Netezza Enterprise
'ODBCConnectorPX'                : '^odbc[A-Z0-9][A-Za-z0-9|_]*', // ODBC Connector
'PxOdbc'                         : '^odbc[A-Z0-9][A-Za-z0-9|_]*', // ODBC Enterprise
'OracleConnectorPX'              : '^ora[A-Z0-9][A-Za-z0-9|_]*' , // Oracle Connector
'PxOracle'                       : '^ora[A-Z0-9][A-Za-z0-9|_]*' , // Oracle Enterprise
'ORAOCIBLPX'                     : '^ora[A-Z0-9][A-Za-z0-9|_]*' , // Oracle OCI Load has been DEPRECATED
'rdbloadPX'                      : '^rb[A-Z0-9][A-Za-z0-9|_]*'  , // RedBrick Load
'SnowflakeConnectorPX'           : '^sn[A-Z0-9][A-Za-z0-9|_]*'  , // Snowflake Connector
'Pxsqlsvr'                       : '^sql[A-Z0-9][A-Za-z0-9|_]*' , // SQLServer Enterprise
'STPPX'                          : '^stp[A-Z0-9][A-Za-z0-9|_]*' , // Stored Procedure
'PxSybase'                       : '^syb[A-Z0-9][A-Za-z0-9|_]*' , // Sybase Enterprise
'IQBulk12PX'                     : '^syb[A-Z0-9][A-Za-z0-9|_]*' , // Sybase IQ 12 Load
'SYBASEOCPX'                     : '^syb[A-Z0-9][A-Za-z0-9|_]*' , // Sybase OC
'TeradataPX'                     : '^tera[A-Z0-9][A-Za-z0-9|_]*', // Teradata API has been DEPRECATED
'TeradataConnectorPX'            : '^tera[A-Z0-9][A-Za-z0-9|_]*', // Teradata Connector
'PxTeradata'                     : '^tera[A-Z0-9][A-Za-z0-9|_]*', // Teradata Enterprise
'TerabulkPX'                     : '^tera[A-Z0-9][A-Za-z0-9|_]*', // Teradata Load has been DEPRECATED
'TDMLoadPX'                      : '^tera[A-Z0-9][A-Za-z0-9|_]*', // Teradata Multiload
// Debug ----------------------------------------------------------------------
'PxColumnGenerator'              : '^cg[A-Z0-9][A-Za-z0-9|_]*'  , // Column Generator
'PxHead'                         : '^hd[A-Z0-9][A-Za-z0-9|_]*'  , // Head
'PxPeek'                         : '^pk[A-Z0-9][A-Za-z0-9|_]*'  , // Peek
'PxRowGenerator'                 : '^rg[A-Z0-9][A-Za-z0-9|_]*'  , // Row Generator
'PxSample'                       : '^sp[A-Z0-9][A-Za-z0-9|_]*'  , // Sample
'PxTail'                         : '^tl[A-Z0-9][A-Za-z0-9|_]*'  , // Tail
'PxWriteRangeMap'                : '^wrm[A-Z0-9][A-Za-z0-9|_]*' , // Write Range Map
// File -----------------------------------------------------------------------
'AzureBlobStorageConnectorPX'    : '^az[A-Z0-9][A-Za-z0-9|_]*'  , // Azure Blob Storage Connector
'AzureFileStorageConnectorPX'    : '^az[A-Z0-9][A-Za-z0-9|_]*'  , // Azure File Storage Connector
'AzureStorageConnectorPX'        : '^az[A-Z0-9][A-Za-z0-9|_]*'  , // Azure Storage Connector
'AmazonS3PX'                     : '^s3[A-Z0-9][A-Za-z0-9|_]*'  , // Amazon S3
'cloudobjectstoragePX'           : '^cos[A-Z0-9][A-Za-z0-9|_]*' , // Cloud Object Storage
'PxCFF'                          : '^cff[A-Z0-9][A-Za-z0-9|_]*' , // Complex Flat File
'PxDataSet'                      : '^ds[A-Z0-9][A-Za-z0-9|_]*'  , // Data Set
'PxExternalSource'               : '^exs[A-Z0-9][A-Za-z0-9|_]*' , // External Source
'PxExternalTarget'               : '^ext[A-Z0-9][A-Za-z0-9|_]*' , // External Target
'FileConnectorPX'                : '^fcon[A-Z0-9][A-Za-z0-9|_]*', // File Connector
'LocalFileConnectorPX'           : '^fcoe[A-Z0-9][A-Za-z0-9|_]*', // File Connector - Engine Tier
'HDFSFileConnectorPX'            : '^fcoh[A-Z0-9][A-Za-z0-9|_]*', // File Connector - HDFS
'PxFileSet'                      : '^fs[A-Z0-9][A-Za-z0-9|_]*'  , // FileSet
'PxLookupFileSet'                : '^luf[A-Z0-9][A-Za-z0-9|_]*' , // Lookup FileSet
'PxSequentialFile'               : '^sq[A-Z0-9][A-Za-z0-9|_]*'  , // Sequential File
'UnstructuredDataConnectorPX'    : '^ud[A-Z0-9][A-Za-z0-9|_]*'  , // Unstructured Data
'PxzOSFile'                      : '^zos[A-Z0-9][A-Za-z0-9|_]*' , // zOSFile
// Packs ----------------------------------------------------------------------
'EssbaseConnectorPX'             : '^ess[A-Z0-9][A-Za-z0-9|_]*' , // Essbase Connector
'PS_HRYPX'                       : '^hpe[A-Z0-9][A-Za-z0-9|_]*' , // Hierarchy for PeopleSoft Enterprise
'PeoplesoftOnePX'                : '^jde[A-Z0-9][A-Za-z0-9|_]*' , // JD Edwards EnterpriseOne
'ORAAppsPX'                      : '^oad[A-Z0-9][A-Za-z0-9|_]*' , // Oracle Applications Direct Access
'orahrchy_PX'                    : '^oah[A-Z0-9][A-Za-z0-9|_]*' , // Oracle Applications Hierarchy
'SALESFORCEJCConnectorPX'        : '^sf[A-Z0-9][A-Za-z0-9|_]*'  , // Salesforce
'Siebel_BCPX'                    : '^sbbc[A-Z0-9][A-Za-z0-9|_]*', // Siebel BC Pack
'Siebel_DAPX'                    : '^sbda[A-Z0-9][A-Za-z0-9|_]*', // Siebel DA Pack
'Siebel_EIMPX'                   : '^sieb[A-Z0-9][A-Za-z0-9|_]*', // Siebel EIM Pack
// Processing -----------------------------------------------------------------
'CTransformerStage'              : '^tx[A-Z0-9][A-Za-z0-9|_]*'  , // Transformer
'PxSVTransformer'                : '^txb[A-Z0-9][A-Za-z0-9|_]*' , // BASIC Transformer
'PxAggregator'                   : '^ag[A-Z0-9][A-Za-z0-9|_]*'  , // Aggregator
'PxBLM'                          : '^blm[A-Z0-9][A-Za-z0-9|_]*' , // Bloomfilter
'PxChangeApply'                  : '^ca[A-Z0-9][A-Za-z0-9|_]*'  , // Change Apply
'PxChangeCapture'                : '^cc[A-Z0-9][A-Za-z0-9|_]*'  , // Change Capture
'PxChecksum'                     : '^cs[A-Z0-9][A-Za-z0-9|_]*'  , // Checksum
'PxCompare'                      : '^cmp[A-Z0-9][A-Za-z0-9|_]*' , // Compare
'PxCompress'                     : '^zip[A-Z0-9][A-Za-z0-9|_]*' , // Compress
'PxCopy'                         : '^cp[A-Z0-9][A-Za-z0-9|_]*'  , // Copy
'DMConnectorPX'                  : '^dm[A-Z0-9][A-Za-z0-9|_]*'  , // Data Masking  
'PxDecode'                       : '^dc[A-Z0-9][A-Za-z0-9|_]*'  , // Decode
'PxDifference'                   : '^df[A-Z0-9][A-Za-z0-9|_]*'  , // Difference
'PxEncode'                       : '^ec[A-Z0-9][A-Za-z0-9|_]*'  , // Encode
'PxExpand'                       : '^uzp[A-Z0-9][A-Za-z0-9|_]*' , // Expand
'PxExternalFilter'               : '^ef[A-Z0-9][A-Za-z0-9|_]*'  , // External Filter
'PxFilter'                       : '^ft[A-Z0-9][A-Za-z0-9|_]*'  , // Filter
'PxFTP'                          : '^ftp[A-Z0-9][A-Za-z0-9|_]*' , // FTP Enterprise
'ftpPX'                          : '^ftp[A-Z0-9][A-Za-z0-9|_]*' , // FTP Plug-in
'PxFunnel (Continuous)'          : '^fc[A-Z0-9][A-Za-z0-9|_]*'  , // Funnel
'PxFunnel (Sort)'                : '^fo[A-Z0-9][A-Za-z0-9|_]*'  , // Funnel
'PxFunnel (Sequence)'            : '^fq[A-Z0-9][A-Za-z0-9|_]*'  , // Funnel
'PxGeneric'                      : '^gn[A-Z0-9][A-Za-z0-9|_]*'  , // Generic
'PxJoin (Inner)'                 : '^ji[A-Z0-9][A-Za-z0-9|_]*'  , // Inner join
'PxJoin (Full Outer)'            : '^jf[A-Z0-9][A-Za-z0-9|_]*'  , // Full Outer join
'PxJoin (Left Outer)'            : '^jl[A-Z0-9][A-Za-z0-9|_]*'  , // Left Outer join
'PxJoin (Right Outer)'           : '^jr[A-Z0-9][A-Za-z0-9|_]*'  , // Right Outer join
'PxLookup'                       : '^lu[A-Z0-9][A-Za-z0-9|_]*'  , // Lookup
'PxMerge'                        : '^mg[A-Z0-9][A-Za-z0-9|_]*'  , // Merge
'PxModify'                       : '^md[A-Z0-9][A-Za-z0-9|_]*'  , // Modify
'PivotPX'                        : '^pv[A-Z0-9][A-Za-z0-9|_]*'  , // Pivot
'PxPivot'                        : '^pv[A-Z0-9][A-Za-z0-9|_]*'  , // Pivot Enterprise
'PxRemDup'                       : '^rd[A-Z0-9][A-Za-z0-9|_]*'  , // Remove Duplicates
'PxSCD'                          : '^scd[A-Z0-9][A-Za-z0-9|_]*' , // Slowly Changing Dimension
'PxSort (Standard)'              : '^so[A-Z0-9][A-Za-z0-9|_]*'  , // Standard Sort
'PxSort (Unique)'                : '^su[A-Z0-9][A-Za-z0-9|_]*'  , // Unique Sort
'PxSurrogateKeyGenerator'        : '^sk[A-Z0-9][A-Za-z0-9|_]*'  , // Surrogate Key Generator (1)
'PxSurrogateKeyGeneratorN'       : '^sk[A-Z0-9][A-Za-z0-9|_]*'  , // Surrogate Key Generator (2)
'PxSwitch'                       : '^sw[A-Z0-9][A-Za-z0-9|_]*'  , // Switch
'PxWaveGenerator'                : '^wg[A-Z0-9][A-Za-z0-9|_]*'  , // Wave Generator
// Real Time ------------------------------------------------------------------
'CDCTStagePX'                    : '^cdc[A-Z0-9][A-Za-z0-9|_]*' , // CDC Transaction
'XMLStagePX'                     : '^hdx[A-Z0-9][A-Za-z0-9|_]*' , // Hierarchical Data
'ILOGJRulesConnectorPX'          : '^ij[A-Z0-9][A-Za-z0-9|_]*'  , // ILOG JRules Connector
'PxRTIInput'                     : '^isi[A-Z0-9][A-Za-z0-9|_]*' , // ISD Input
'PxRTIOutput'                    : '^iso[A-Z0-9][A-Za-z0-9|_]*' , // ISD Output
'JClientPX'                      : '^jc[A-Z0-9][A-Za-z0-9|_]*'  , // Java Client
'JavaStagePX'                    : '^jint[A-Z0-9][A-Za-z0-9|_]*', // Java Integration
'JTransformerPX'                 : '^jt[A-Z0-9][A-Za-z0-9|_]*'  , // Java Transformer
'JAQLConnectorPX'                : '^mr[A-Z0-9][A-Za-z0-9|_]*'  , // MapReduce Connector
'StreamsConnectorPX'             : '^str[A-Z0-9][A-Za-z0-9|_]*' , // Streams Connector
'WSClientPX'                     : '^wsc[A-Z0-9][A-Za-z0-9|_]*' , // Web Services Client
'WSTransformerPX'                : '^wst[A-Z0-9][A-Za-z0-9|_]*' , // Web Services Transformer
'MQSeriesPX'                     : '^mq[A-Z0-9][A-Za-z0-9|_]*'  , // WebSphere MQ Stage has been DEPRECATED
'WebSphereMQConnectorPX'         : '^mq[A-Z0-9][A-Za-z0-9|_]*'  , // WebSphere MQ Connector
'XMLInputPX'                     : '^xmi[A-Z0-9][A-Za-z0-9|_]*' , // XML Input
'XMLOutputPX'                    : '^xmo[A-Z0-9][A-Za-z0-9|_]*' , // XML Output
'XMLTransformerPX'               : '^xmt[A-Z0-9][A-Za-z0-9|_]*' , // XML Transformer
// Restructure ----------------------------------------------------------------
'PxColumnExport'                 : '^ce[A-Z0-9][A-Za-z0-9|_]*'  , // ColumnExport
'PxColumnImport'                 : '^ci[A-Z0-9][A-Za-z0-9|_]*'  , // ColumnImport
'PxCombineRecords'               : '^cb[A-Z0-9][A-Za-z0-9|_]*'  , // CombineRecords
'PxMakeSubRec'                   : '^msr[A-Z0-9][A-Za-z0-9|_]*' , // MakeSub-Record
'PxMakeVect'                     : '^mvt[A-Z0-9][A-Za-z0-9|_]*' , // MakeVector
'PxPromoteSubRec'                : '^psr[A-Z0-9][A-Za-z0-9|_]*' , // PromoteSub-Record
'PxSplitSubRec'                  : '^ssr[A-Z0-9][A-Za-z0-9|_]*' , // SplitSub-Record
'PxSplitVect'                    : '^svt[A-Z0-9][A-Za-z0-9|_]*' , // SplitVector
// Containers -----------------------------------------------------------------
'Container (Local)'              : '^lc[A-Z0-9][A-Za-z0-9|_]*'  , // Local Container
'Container (Shared)'             : '^sc[A-Z0-9][A-Za-z0-9|_]*'    // Shared Container
```

## Server Job Stages

```
// Server Database ------------------------------------------------------------
'DB2Connector'                   : '^db2[A-Z0-9][A-Za-z0-9|_]*'  , // Ibm Infosphere DB2 Connector
'DSDB2'                          : '^db2[A-Z0-9][A-Za-z0-9|_]*'  , // DB2 Stage has been DEPRECATED - Replaced By The DB2 Connector Stage
'UDBLoad'                        : '^db2[A-Z0-9][A-Za-z0-9|_]*'  , // DB2 UDB Load has been DEPRECATED - Replaced By The DB2 Connector Stage
'DRS'                            : '^drs[A-Z0-9][A-Za-z0-9|_]*'  , // Dynamic RDBMS Stage has been DEPRECATED - Replaced By the Dynamic RDBMS Connector Stage
'DRSConnector'                   : '^drs[A-Z0-9][A-Za-z0-9|_]*'  , // Dynamic RDBMS Connector
'InfmxCLI'                       : '^ifx[A-Z0-9][A-Za-z0-9|_]*'  , // Informix Data Access
'INFBLK10'                       : '^ifx[A-Z0-9][A-Za-z0-9|_]*'  , // Informix Bulk Loader
'XPSLoad'                        : '^xps[A-Z0-9][A-Za-z0-9|_]*'  , // Informix XPS Bulk Loader
'NetezzaConnector'               : '^net[A-Z0-9][A-Za-z0-9|_]*'  , // Netezza Connector
'CODBCStage'                     : '^odbc[A-Z0-9][A-Za-z0-9|_]*' , // ODBC Data Access
'ODBCConnector'                  : '^odbc[A-Z0-9][A-Za-z0-9|_]*' , // IBM Infosphere ODBC Connector
'ORABULK'                        : '^ora[A-Z0-9][A-Za-z0-9|_]*'  , // Oracle Bulk Loader
'OracleConnector'                : '^ora[A-Z0-9][A-Za-z0-9|_]*'  , // Oracle Connector
'ORAOCI9'                        : '^ora[A-Z0-9][A-Za-z0-9|_]*'  , // Oracle OCI Stage has been DEPRECATED - Replaced By The Oracle Connector Stage
'ORAOCIBL'                       : '^ora[A-Z0-9][A-Za-z0-9|_]*'  , // Oracle OCI Bulk Loader Stage has been DEPRECATED - Replaced By The Oracle Connector Stage
'rdbload'                        : '^rb[A-Z0-9][A-Za-z0-9|_]*'   , // Redbrick Bulk Loader
'STP'                            : '^stp[A-Z0-9][A-Za-z0-9|_]*'  , // The Stored Procedure Stage
'BCPLOAD'                        : '^bcp[A-Z0-9][A-Za-z0-9|_]*'  , // Sybase Sql Server Bulk Loader
'IQBulk12'                       : '^syb[A-Z0-9][A-Za-z0-9|_]*'  , // Sybase IQ 12 Bulk Loader
'SYBASEOC'                       : '^syb[A-Z0-9][A-Za-z0-9|_]*'  , // Sybase Data Access
'Teradata'                       : '^tera[A-Z0-9][A-Za-z0-9|_]*' , // Teradata Stage has been DEPRECATED - Replaced By The Teradata Connector Stage
'TeradataConnector'              : '^tera[A-Z0-9][A-Za-z0-9|_]*' , // IBM Infosphere Teradata Connector
'Terabulk'                       : '^tera[A-Z0-9][A-Za-z0-9|_]*' , // Teradata Bulk Stage has been DEPRECATED - Replaced By The Teradata Connector Stage
'TDMLoad'                        : '^tera[A-Z0-9][A-Za-z0-9|_]*' , // Teradata Multiload/Tpump/Fastexport Stage.
'CUniDataStage'                  : '^ud[A-Z0-9][A-Za-z0-9|_]*'   , // Unidata Data Access
'CUvStage'                       : '^uv[A-Z0-9][A-Za-z0-9|_]*'   , // Universe Data Access
// Server File ----------------------------------------------------------------
'CFF'                            : '^cff[A-Z0-9][A-Za-z0-9|_]*'  , // Complex Flat File Stage.
'Folder'                         : '^fol[A-Z0-9][A-Za-z0-9|_]*'  , // Read Or Write Data As Files In A Directory
'CHashedFileStage'               : '^hf[A-Z0-9][A-Za-z0-9|_]*'   , // Typically A Keyed Reference File
'CSeqFileStage'                  : '^seq[A-Z0-9][A-Za-z0-9|_]*'  , // Sequential Data Access
// Server Packs ---------------------------------------------------------------
'PS_HRY'                         : '^hpe[A-Z0-9][A-Za-z0-9|_]*'  , // Peoplesoft Enterprise Hierarchy Plug-In
'PeoplesoftOne'                  : '^jde[A-Z0-9][A-Za-z0-9|_]*'  , // JD Edwards Enterprise One Stage
'ORAApps'                        : '^oad[A-Z0-9][A-Za-z0-9|_]*'  , // Oracle Applications Direct Access Stage
'orahrchy'                       : '^oah[A-Z0-9][A-Za-z0-9|_]*'  , // Oracle Applications Hierarchy Stage
'Siebel_BC'                      : '^sbbc[A-Z0-9][A-Za-z0-9|_]*' , // Siebel Business Component Access Stage
'Siebel_DA'                      : '^sbda[A-Z0-9][A-Za-z0-9|_]*' , // Siebel Direct Access Stage Version 3.2.2
'Siebel_EIM'                     : '^sieb[A-Z0-9][A-Za-z0-9|_]*' , // Siebel Stage
// Server Processing ----------------------------------------------------------
'AGGREGATOR'                     : '^ag[A-Z0-9][A-Za-z0-9|_]*'   , // Form Groups Or Perform Other Aggregate Functions
'ftp'                            : '^ftp[A-Z0-9][A-Za-z0-9|_]*'  , // FTP Data Access
'CInterProcess'                  : '^ipc[A-Z0-9][A-Za-z0-9|_]*'  , // Communication Channel Between Stages
'CCollector'                     : '^col[A-Z0-9][A-Za-z0-9|_]*'  , // Merge Up To 64 Links Into Single Output Link
'CPartitioner'                   : '^par[A-Z0-9][A-Za-z0-9|_]*'  , // Partition Data Out To Multiple Links
'MERGE'                          : '^mg[A-Z0-9][A-Za-z0-9|_]*'   , // Merge Data Access
'Pivot'                          : '^pv[A-Z0-9][A-Za-z0-9|_]*'   , // Pivot Plugin Version 1.0.0
'RowMerger'                      : '^rm[A-Z0-9][A-Za-z0-9|_]*'   , // Row Merger Active Plug-In Stage
'RowSplitter'                    : '^rs[A-Z0-9][A-Za-z0-9|_]*'   , // Row Splitter Active Plug-In Stage
'sort'                           : '^so[A-Z0-9][A-Za-z0-9|_]*'   , // Sort
// Server Real-Time -----------------------------------------------------------
'RTIInput'                       : '^isi[A-Z0-9][A-Za-z0-9|_]*'  , // Information Services Input Stage
'RTIOutput'                      : '^iso[A-Z0-9][A-Za-z0-9|_]*'  , // Information Services Output Stage
'JClient'                        : '^jc[A-Z0-9][A-Za-z0-9|_]*'   , // Transformer For Java Passive Plug-In Stage
'JTransformer'                   : '^jt[A-Z0-9][A-Za-z0-9|_]*'   , // Transformer For Java Active Plug-In Stage
'WSClient'                       : '^wsc[A-Z0-9][A-Za-z0-9|_]*'  , // Passive Web Service Plug-In Stage
'WSTransformer'                  : '^wst[A-Z0-9][A-Za-z0-9|_]*'  , // Active Web Service Plug-In Stage
'WebSphereMQConnector'           : '^mq[A-Z0-9][A-Za-z0-9|_]*'   , // IBM Websphere MQ Connector
'XMLInput'                       : '^xmi[A-Z0-9][A-Za-z0-9|_]*'  , // XML Input Stage
'XMLOutput'                      : '^xmo[A-Z0-9][A-Za-z0-9|_]*'  , // XML Output Stage
'XMLTransformer'                 : '^xmt[A-Z0-9][A-Za-z0-9|_]*'  , // XML Transformer Stage
// Containers -----------------------------------------------------------------
'Container (Local)'              : '^lc[A-Z0-9][A-Za-z0-9|_]*'   , // Local Container
'Container (Shared)'             : '^sc[A-Z0-9][A-Za-z0-9|_]*'   , // Shared Container
// All Processing -------------------------------------------------------------
'CTransformerStage'              : '^tx[A-Z0-9][A-Za-z0-9|_]*'     // Transformer
```

## Job Sequence Activities

```
// Sequences  -----------------------------------------------------------------
'CCondition'                      : '^con[A-Z0-9][A-Za-z0-9|_]*' , // Condition
'CEndLoopActivity'                : '^le[A-Z0-9][A-Za-z0-9|_]*'  , // End Loop Activity
'CExceptionHandler'               : '^exc[A-Z0-9][A-Za-z0-9|_]*' , // Exception Handler
'CExecCommandActivity'            : '^com[A-Z0-9][A-Za-z0-9|_]*' , // Execute Command Activity
'CJobActivity'                    : '^job[A-Z0-9][A-Za-z0-9|_]*' , // Job Activity
'CNotificationActivity'           : '^not[A-Z0-9][A-Za-z0-9|_]*' , // Notification Activity
'COozieWfActivity'                : '^ooz[A-Z0-9][A-Za-z0-9|_]*' , // Oozie Workflow
'CRoutineActivity'                : '^rt[A-Z0-9][A-Za-z0-9|_]*'  , // Routine Activity
'CSequencer'                      : '^seq[A-Z0-9][A-Za-z0-9|_]*' , // Job Sequence
'CStartLoopActivity'              : '^ls[A-Z0-9][A-Za-z0-9|_]*'  , // Start Loop Activity
'CTerminatorActivity'             : '^ter[A-Z0-9][A-Za-z0-9|_]*' , // Terminator Activity
'CUserVarsActivity'               : '^usr[A-Z0-9][A-Za-z0-9|_]*' , // User Variables Activity
'CWaitForFileActivity'            : '^wff[A-Z0-9][A-Za-z0-9|_]*'   // Wait For File Activity
```

## Blocklist

MettleCI also ships with [a Compliance Rule](../../compliance-testing/mettleci-compliance-rules-reference/job-naming.md) which identifies jobs with names that suggest that they are not intended as production candidates. This rule ships with an in-built list is applied to Parallel, Server, and Sequence asset types. You can configure the list by editing the definition of the relevant Compliance Rule. e.g.,

```
  // Job names indicating they are not intended for production
 '^(?i)CopyOf.*',     //Job Name starts with 'CopyOf'
  '^(?i)Untitled.*',  //Job Name starts with 'Untitled'  
  '(?i).*_WIP$',      //Job Name ends with '_WIP'
  '(?i).*DEBUG$',     //Job Name ends with 'DEBUG'
  '(?i).*ORIGINAL$',  //Job Name ends with 'ORIGINAL'
  '(?i).*TEMP$',      //Job Name ends with 'TEMP'
  '(?i).*TMP$',       //Job Name ends with 'TMP'
  // Job names using dates
  '.*[12]\\d{3}(0[1-9]|1[0-2])(0[1-9]|[12]\\d|3[01]).*', //YYYYMMDD
  '.*(0[1-9]|[12]\\d|3[01])(0[1-9]|1[0-2])[12]\\d{3}.*', //DDMMYYYY
  '.*(0[1-9]|1[0-2])(0[1-9]|[12]\\d|3[01])[12]\\d{3}.*', //MMDDYYYY
  '.*\\d{2}(0[1-9]|1[0-2])(0[1-9]|[12]\\d|3[01]).*',     //YYMMDD
  '.*(0[1-9]|[12]\\d|3[01])(0[1-9]|1[0-2])\\d{2}.*',     //DDMMYY
  '.*(0[1-9]|1[0-2])(0[1-9]|[12]\\d|3[01])\\d{2}.*'      //MMDDYY
```