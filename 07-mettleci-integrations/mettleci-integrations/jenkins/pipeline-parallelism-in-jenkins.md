# Pipeline Parallelism in Jenkins

# Introduction

One of the key goals of Continuous Integration is to support a [**shift left**](https://en.wikipedia.org/wiki/Shift-left_testing) testing philosophy which provides Developers with fast feedback on the quality of their code changes. This is achieved, in part, by the use of fast, tightly-scoped tests, triggered quickly after a change is detected. As such, the speed of the Continuous Integration testing process is of paramount importance. This speed can be optimised using a number of methods, the most effective of which are…

*   Minimise the scope of the tests being performed (e.g. by avoiding the dynamic provisioning of environments or sizeable volumes of data), and
    
*   Execute the CI tests as quickly as possible, running testing steps in parallel where at all possible.
    

This page describes how to configure the latter in Jenkins.

# MettleCI Use Cases

In MettleCI the obvious candidates for parallel test execution are:

*   Compliance Testing (for Warnings),
    
*   Compliance Testing (for Failures), and
    
*   Unit Tests
    

Each of these can be performed concurrently without affecting the other as the Compliance processes run independently in memory using a data from supplied files, while the Unit Test runs in the DataStage environment as one or more executing Jobs.

# Parallelism in Jenkins

Parallelism in Jenkins is defined at the Stage level which means that a single Jenkins Pipeline is invoked, containing…

*   Some Stages configured to run **sequentially** (with their component Steps running sequentially), and/or
    
*   Some Stages configured to run **concurrently** (with their component Steps running sequentially)
    

See [Parallel stages with Declarative Pipeline 1.2 (jenkins.io)](https://www.jenkins.io/blog/2017/09/25/declarative-1/#parallel-stages)

# Defining Parallel Stages in a Jenkins Pipeline

Here’s a pseudocode representation of two parallel Stages defined in a Jenkins Pipeline. It runs the following stages concurrently:

*   A test (Windows command line) on any Jenkins Agent with a ‘windows’ label, and
    
*   A test (Unix shell) on any Jenkins Agent with a ‘linux’ label
    

```
pipeline {
    stages {
        stage('Do These Concurrently') {
            parallel {
                stage('Test On Windows') {
                    agent {
                        label "windows"
                    }
                    steps {
                        bat "run-tests.bat"
                    }
                    post {
                        always {
                            junit "**/TEST-*.xml"
                        }
                    }
                }
                stage('Test On Linux') {
                    agent {
                        label "linux"
                    }
                    steps {
                        sh "run-tests.sh"
                    }
                    post {
                        always {
                            junit "**/TEST-*.xml"
                        }
                    }
                }
            }
        }
    }
}
```