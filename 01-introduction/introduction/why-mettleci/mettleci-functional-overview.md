# MettleCI Functional Overview

# Introduction

This document provides an objective, factual description of the features and functions of Data Migrators' MettleCI DevOps platform for IBM Information Server.

*   [Introduction](#introduction)
*   [Origins and Intent](#origins-and-intent)
*   [MettleCI Benefits](#mettleci-benefits)
*   [MettleCI Features & Functions](#mettleci-features-functions)
*   [Documentation and Support](#documentation-and-support)
*   [System Features](#system-features)
*   [User Interfaces](#user-interfaces)
*   [Communication Interfaces](#communication-interfaces)
*   [Non-functional Requirements](#non-functional-requirements)

# Origins and Intent

MettleCI was born as a collection of custom-built tools and utilities created by Data Migrators Pty Ltd. These tools were born out of a Data Migrators' desire to improve the speed, quality, traceability, and efficiency of its professional services when delivering solutions founded on IBM information Server DataStage.

# MettleCI Benefits

*   Shorter time to delivery
    
*   Lower cost of maintenance
    
*   Higher performance Jobs
    
*   Earlier, cheaper defect discovery
    
*   Lower testing costs
    
*   More reliable E2E execution
    
*   Zero-effort work item traceability
    
*   Release management with minimal effort
    
*   Visibly more productive DataStage teams
    
*   Higher utilisation of Information Server platform
    
*   Demonstrable alignment with organisation strategy
    

# MettleCI Features & Functions

*   Automated Peer Review (Compliance)
    
*   Automated Unit Testing (generation & management)
    
*   Universal Git integration (Jobs and Unit Tests)
    
*   Continuous Integration
    
*   Continuous Delivery
    
*   Automated bulk update of job designs and settings
    

# Documentation and Support

All MettleCI documentation is kept up to date and made publicly available at [http://docs.mettleci.io](http://docs.mettleci.io/).

Information on procurement and support is available [here](https://datamigrators.atlassian.net/wiki/spaces/MCIDOC/pages/454131717/Procurement+and+Licensing).

# System Features

| **Feature** | **Description** | **Stimulus / Response** | **Functional Requirements** |
| --- | --- | --- | --- |
| Automated Peer Review ('Compliance') | Compliance rules are executed every time a DataStage job is checked in. A compliance test comprises a static (non-executing) evaluation of the DataStage job against a set of development rules. These rules can include constraints on job naming, link naming, stage naming, stage property values, stage relationships (such as stage adjacency) as well as defining mandatory or prohibited stage types for different job types. For example, the presence of links named DSLinkN, hardcoded Dataset paths (which don't utilise a parameter value for their path), or the presence of adjacent Transforms are all examples of anti-patterns MettleCI can check for.<br><br>MettleCI ships with a comprehensive set of best-practice compliance rules which are easily adapted or extended by MettleCI customers. The compliance rules are stored in Customer's Git-based Bitbucket repository. Compliance rules can be global (applying to all projects under the management of a MettleCI instance), specific to a particular project, or applied to individual jobs with names matching a supplied regular expression. Any new compliance rules submitted from a project team to the global repository would be issued as a pull request that a governance team can review before merging to the global compliance repository. | **Stimulus:** User creates or edits a compliance rule (or its associated test DataStage artefact) in the compliance rule repository. **Response:** A build plan is executed which tests the newly created/updated compliance rule against a test DataStage artefact.<br><br>**Stimulus:** User invokes a compliance check against one or more DataStage artefacts using the MettleCI Workbench User Interface. **Response:** All specified artefacts are tested against all compliance rules currently available in the compliance rule repository. | **Com1:** The system provides an ability to associate a DataStage project with a Git repository containing the compliance rules against which jobs in the DataStage project will be assessed.<br><br>**Com2:** The system permits the specification of compliance rules using a version of the Apache Gremlin graph traversal language enhanced to support DataStage terminology like 'stage' and ‘link'.<br><br>**Com3:** The system supports the storage of compliance rules in a Git repository.<br><br>**Com4:** The system permits the testing of compliance rules against one or more DataStage artefacts (Parallel jobs, Server jobs, and Job Sequences)<br><br>**Com5:** The system permits the testing of jobs' compliance with compliance rules as part of a CI/CD pipeline.<br><br>**Com6:** The system permits the classification of compliance rules into ‘Warning’ and ‘Fatal’, where only non-compliance with ‘Fatal’ rules causes CI/CD pipeline failure.<br><br>**Com7:** The system provides a pre-populated library of compliance rules which embody development standards and approaches considered by a panel of DataStage experts as ‘best practice’.<br><br>**Com8:** The system provides the ability to expose Compliance Test results in a jUnit-compatible form. |
| Automated Unit Testing | MettleCI provides a comprehensive and sophisticated automated Unit Testing capability. The focus of MettleCI Unit Testing is to create and publish (to Git) a set of artefacts (test specifications and associated test data) that embody a definition of (used to demonstrate) your job's correct functional behaviour. These artefacts can be propagated to downstream environments where they can be used to verify your job's consistent behaviour on DataStage platforms which may not have the same configuration, connectivity, or even DataStage version as the project in which the original job was developed.<br><br>The Unit being tested by MettleCI's Unit Test capability is an individual DataStage job. Test data can be derived using a number of methods, each of which may be used in combination with one another:<br><br>1.  Entered manually into the Excel-like test data file tables in MettleCI Workbench<br>    <br>2.  Provided as CSV file which are imported into the relevant test data file using MettleCI Workbench<br>    <br>3.  Fabricated using MettleCI Workbench's Data Fabrication capabilities (see below)<br>    <br>4.  Captured from your existing unit test data sources using MettleCI's Data Interception capabilities (see below) | **Stimulus:** User requests the creation of a unit test for a DataStage job. **Response:** A formal unit test specification is automatically generated along with references to a set of input test data, and expected output data files which are also generated as empty files containing corresponding data columns of the appropriate names and datatypes.<br><br>**Stimulus:** User invokes a DataStage job execution providing the MettleCI Unit Testing parameter with a value of ‘Testing’. **Response:** The job is intercepted at runtime and dynamically rewritten to replace source and target stages with custom components which inject the contents of the MettleCI Unit Test input Test Data Files referenced by the associated Unit Test Specification. Data flowing to the output stage(s) are intercepted and compared to the contents of the MettleCI Unit Test output Test Data Files. A different report between expected actual output is produced.<br><br>**Stimulus:** User requests the deletion of a unit test for a DataStage job. **Response:** The unit test specification and its referenced input and output data files are deleted from the filesystem. | **UT1:** The system provides an ability to associate a DataStage project with a Git repository which will be used to contain the MettleCI Unit Test artefacts associated with the DataStage project’s jobs.<br><br>**UT2:** The system permits the definition of a formal unit test specification using a YAML-based notation similar in structure to the Gherkin notation employed by the popular Cucumber automated test tool. This notation links a job, its parameters, a specified set of input test data, and a specified set of expected output data into a single artefact.<br><br>**UT3:** The system permits the definition of unit test input data and unit test expected output data linked to a unit test specification.<br><br>**UT4:** The system provides a facility to automatically generate the unit test specification YAML as well as empty template files to contain the set of required input test data and expected output data.<br><br>**UT5:** The system permits the execution of a unit test case which supplies the Unit Test input data to a DataStage job, regardless of input stage type(s), and compares output(s) to the expected output and produced a report detailing the differences.<br><br>**UT6:** The system provides the ability to expose Unit Test results in a jUnit-compatible form. |
| Test Data Fabrication | Fabricated using MettleCI Workbench's Data Fabrication capabilities (see below) | **Stimulus:** When editing a Unit Test input Data File using the MettleCI workbench the User modifies the properties of a selected column to specify a fabrication type for that column. **Response:** The column is populated with fictional, yet authentic-looking, data based on the selected fabrication type. | **Fab1:** The system provides a library of functions which can be employed by the user to specify fictional yet authentic-looking data for use in Unit Test input Data Files. |
| Test Data Interception | MettleCI provides the capability to intercept input and output data flowing through a job and use this as the input and expected output of an automated Unit Test case. | **Stimulus:** User invokes a DataStage job execution providing the MettleCI Unit Testing parameter with a value of ‘Interception’. **Response:** The data flowing along the job’s input and output links is intercepted at runtime can replicated into the contents of the MettleCI Unit Test input and output Test Data Files referenced by the associated Unit Test Specification. | **Inter1:** The system permits the interception and capture of data flowing through a DataStage job for later use within the Unit Test Function as input data and expected output data files. |
| Universal Git integration | MettleCI enables you to check in changed DataStage Repository-based assets (e.g. Jobs, ParameterSets...) to any vendor’s Git-compatible software repository. Git check-ins can be performed either via a combination of the DataStage Classic Designer client and MettleCI Workbench or directly in MettleCI Workbench. | **Stimulus:** User invokes a Git Check-in using the MettleCI Workbench, specifying one or more DataStage artefacts, whether or not the check-in should include any associated Unit Test assets, one or more references to work items in an associated work item management system, and a commit message. **Response:** The specified DataStage assets and unit test artefacts are checked in to git along with the supplied work item references and commit message.<br><br>**Stimulus:** User enters the reference or partial title of a work item in their MettleCI project’s associated Atlassian Jira or Azure DevOps work item management system. **Response:** The work item management system is dynamically queried and the matching work item(s) are presented to the user in a drop-down list. | **Git1:** The system provides an ability to associate a DataStage project with a Git repository which will be used to contain the DataStage artefacts as candidates for Continuous Integration and Deployment process.<br><br>**Git2:** The system provides the ability to check-in one or more specified DataStage artefacts in to a linked Git repository. |
| Continuous Integration, Continuous Delivery | MettleCI provides a number of advanced build and deployment components which can be accessed using proprietary interfaces (currently available for Atlassian Bamboo and Microsoft Azure DevOps) or a generic command line which can be used by any build and deployment technology. | **Stimulus / Response:** Please see [https://datamigrators.atlassian.net/wiki/x/GABXG](https://datamigrators.atlassian.net/wiki/x/GABXG) for a summary of MettleCI’s Continuous Integration and Deployment components. | **CICD1:** Please see [https://datamigrators.atlassian.net/wiki/x/GABXG](https://datamigrators.atlassian.net/wiki/x/GABXG) for a summary of MettleCI’s Continuous Integration and Deployment components. |
| Automated bulk update of job designs and settings | This MettleCI capability takes a specified set of input ISX files and modifies them based on instructions provided in a supplied YAML file. The first public interface to the Transmuter function will be made available from the MettleCI command line. |     |     |

# User Interfaces

*   **MettleCI Workbench:** A browser-based application for the creation, management, and monitoring of Unit Tests, Compliance runs, and Git check-ins.
    
*   **Windows/Unix Command Line:** Windows and Unix command line interfaces into MettleCI’s suite of build and deployment components.
    

# Communication Interfaces

List requirements of communication functions: email, browsers, servers, forms, etc. Describe standards employed, security or encryption measures, data transfer rates, and synching.

*   **MettleCI Workbench API:** A REST API used by the MettleCI workbench to communicate with the MettleCI Workbench service.
    

# Non-functional Requirements

## Performance

*   MettleCI Compliance should be able to test 50 compliance rules against 1 DataStage job in less than 1 second (excluding job export).
    
*   MettleCI Compliance should be able to test 50 compliance rules against 100 DataStage jobs in less than 5 seconds (excluding job export).
    
*   MettleCI should be able to create an automated Unit Test specification and 10 associated template data files for 1 DataStage job in less than 1 second (excluding job export).
    

## Security

MettleCI should not store any of its own credentials, and should utilise either…

*   DataStage credentials, delegating authentication to Information Server, or
    
*   User-supplied public SSH keys for its interaction with third party software