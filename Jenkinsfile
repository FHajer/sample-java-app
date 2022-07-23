pipeline {
    agent any

    environment {


        SONAR_IP = "54.226.50.200"
        SONAR_TOKEN = " sqp_d5d7fd4852745a07f24a8c832d21b380b8a8cc79"

    }

    stages {
        stage('Validate') {
            steps {
                
                sh "mvn validate"

                sh "mvn clean"

            }
        }

         stage('Build') {
            steps {
                
                sh "mvn compile"

            }
        }

        stage('Test') {
            steps {
                
                sh "mvn test"

            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('Quality Scan'){
            steps {
                sh '''

             mvn clean verify sonar:sonar \
                -Dsonar.projectKey=sample-maven-app \
                -Dsonar.host.url=http://54.226.50.200 \
                -Dsonar.login=sqp_d5d7fd4852745a07f24a8c832d21b380b8a8cc79
               

                '''
            }
        }

        stage('Package') {
            steps {
                
                sh "mvn package"

            }

            post {
                success {
                    archiveArtifacts artifacts: '**/target/**.war', followSymlinks: false

                   
                }
            }
        }

        
    }
}