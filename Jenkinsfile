pipeline {
    agent any
        environment {
             appVersion = ''
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
                        // Read the file into a Groovy object
                        def packageJson = readJSON file: 'package.json'
                        appVersion = packageJson.version
                        echo "Package Version: ${appVersion}"
                        }
                    }
                }
            
            stage ('build') {
                steps{
                    script {
                        '''
                        print "hello this is build stage"
                        echo 'we will go to write pipeline for catalogue'

                        '''

                    }

                }

            }
            stage ('test') {
                steps {
                    script {
                        '''
                        print "hello this is test stage"
                        echo 'we will go to write pipeline for catalogue'

                        '''
                    }
                }
            }
            stage ('deploy') {
                steps  {
                    script {
                        '''
                        print "hello this is deploy stage"
                        echo 'we will go to write pipeline for catalogue'

                        '''

                    }

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