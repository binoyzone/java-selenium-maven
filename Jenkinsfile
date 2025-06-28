pipeline
    {
        agent any

                tools
                    {
                        maven 'Maven_3_9_10'
                        jdk 'JDK_21'
                    }
                environment
                    {
                        BROWSER = 'chrome'
                    }
                stages
                    {
                        stage('Checkout')
                            {
                                steps
                                    {
                                        git branch : 'main', url: 'https://github.com/binoyzone/java-selenium-maven'
                                        echo 'Checkout'
                                    }
                            }
                        stage('Build')
                            {
                                steps
                                    {
                                        echo 'Build'
                                        sh 'mvn clean compile'
                                    }
                            }
                        stage('Run Tests')
                            {
                                steps
                                    {
                                        echo 'Test'
                                        sh 'mvn test'
                                    }
                            }
                            stage('Report')
                                {
                                    steps
                                        {
                                            echo 'Report'
                                            junit '**/target/surefire-reports/*.xml'

                                            publishHTML(target: [
                                                                reportDir: 'target/html-report',
                                                                reportFiles: 'index.html',
                                                                reportName: 'Test Report',
                                                                keepAll: true,
                                                                alwaysLinkToLastBuild: true,
                                                                allowMissing: false
                                                            ])
                                        }
                                 }
                         }
                         post
                            {
                                always
                                    {
                                        echo 'Pipeline finished'
                                    }
                                failure
                                    {
                                        echo 'Build failed'
                                    }
                            }
                    }

