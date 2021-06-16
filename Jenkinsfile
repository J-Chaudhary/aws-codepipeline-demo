pipeline {
    agent any
    
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AnkushSinha30/aws-codepipeline-demo.git']]])
            }
        }

        stage('Build') {
            steps {
                nodejs('NodeJS') {
                    sh "yarn install"
                    sh "yarn test"
                    sh "yarn build"
                }
            }
        }
        stage('publish_to_S3') {
          steps {
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'codepipeline-counter-demo30', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-iso-east-1', showDirectlyInBrowser: false, sourceFile: 'dist/*.*', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'myaws', userMetadata: []
                 }
            }
        }
    }
