pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }
    

    stages {
       

      
     
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
              
                git branch: 'master' , url: 'https://github.com/aarsh2211/Microservices'

                // Run Maven on a Unix agent.
                sh "cd api-gateway"
                echo "inside api-gateway"
                sh "mvn clean install"
                
                sh "cd ../eureka-server"
                echo "inside eureka-server"
                sh "mvn clean install"
                
                sh "cd ../message-details-service"
                echo "inside Message details service"
                sh "mvn clean install"
                sh "cd ../message-service"
                echo "inside Message service"
                sh "mvn clean install"
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
