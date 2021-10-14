@Library('shared-AWS-Lib') _
pipeline {
        agent any
        environment {
            AWS_CRED = 'cloud_user'
            AWS_REGION = 'us-east-1'
            templateBucket = 'filesdarren'
            stackName = 'EC2Jenkins-Darren'
        }
        stages {
             stage('Upload Templates') {                  
                steps { 
                        uploadTemplateS3(s3Bucket: "${templateBucket}")
                }
            } 
            stage('Create Bucket') {                  
                steps {
                    createBucket()
                }
            }
            stage('Create DynamoDB') {                  
                steps {
                    createDynamo()
                }
            }
            stage('Upload Files to S3') {                  
                steps {
                    uploadAllFileS3(s3Bucket:"sample-bucket-darren")
                }
            }
            stage('Copy Certain File from another S3') {                  
                steps {
                    copyFileS3(s3fromBucket:"testbucket-abigael", s3Bucket:"sample-bucket-darren")
                }
            }
            stage('Delete a file from S3 bucket') {                  
                steps {
                    deleteFileS3(s3Bucket: "sample-bucket-darren", pathName: "CertainFileSample.txt")
                }
            }
            stage('Deploy EC2') {                  
                steps {
                        deployToEC2(stackName: "${stackName}", s3Bucket: "${templateBucket}")
                }
            }
        }
    }
//scriptSample()
//scriptStages()
