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
                bat "cd api-gateway"
                echo "inside api-gateway"
                bat "mvn clean install"
                
                bat "cd ../eureka-server"
                echo "inside eureka-server"
                bat "mvn clean install"
                
                bat "cd ../message-details-service"
                echo "inside Message details service"
                bat "mvn clean install"
                bat "cd ../message-service"
                echo "inside Message service"
                bat "mvn clean install"
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
