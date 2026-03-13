pipeline {
    agent any
        environment {
             appVersion = ''
             REGION = "us-east-1"
             ACC_ID = "405832638662"
             PROJECT = "roboshop"
             COMPONENT = "catalogue"
        }
        tools {
            git 'Default'
        }
        options{
            disableConcurrentBuilds()
        }
        stages {
            stage('Read package.json') {
                steps {
                    script {
                        def packageJson = readJSON file: 'package.json'
                        appVersion = packageJson.version
                        echo "Package Version: ${appVersion}"
                        }
                    }
                }
            stage ('dependency installation') {
                steps{
                    script {
                        sh '''
                           npm install
                        '''
                    }
                }
            }
            
            stage ('build') {
                steps{
                    script {
                        withAWS(credentials: 'sam-jenkins-demo-credentials', region: 'us-east-1') {
                        sh  '''
                            aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com              
                            docker build -t ${PROJECT}-${COMPONENT}:latest ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}-${COMPONENT}:${appVersion}
                            docker push ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}-${COMPONENT}:${appVersion}

                        '''
                        }

                    }

                }
            }
            stage ('test') {
                steps {
                    script {
                        sh '''
                            echo "hello this is test stage"
                            echo 'we will go to write pipeline for ${COMPONENT}'

                        '''
                    }
                }
            }
            stage ('deploy') {
                steps  {
                    script {
                        sh '''
                            echo "hello this is deploy stage"
                            echo 'we will go to write pipeline for ${COMPONENT}'

                        '''

                    }

                }  
            }
        post {
            success {
                echo "pipeline execution is sucess"
            }
            failure {
                echo "pipeline execution is failed"
            }
        }

    }
}