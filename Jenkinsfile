@Library('my-shared-library') _

//evenOrOdd(currentBuild.getNumber())
//log.info 'Starting'
//log.warning 'Nothing to do!'

pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
            gitCheckout(
                branch: "Feature",
                url: "https://github.com/MyInfosys/ABC.git"
                )
            }
        }
        
        stage ('Compile Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean compile'
                }
            }
        }
        
        stage ('Testing Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                }
            }
        }

         stage ('Run Sonar Analysis Stage on Feature') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh """mvn sonar:sonar \
                         -Dsonar.projectKey=abc_sonar \
                         -Dsonar.host.url=http://35.239.219.161:9000 \
                         -Dsonar.login=7aa0f5eec8f0ef469314e6b95f4c18ce822b0891"""
                }
            }
        }               
                
         stage ('Deploy To Nexus Feature Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn deploy'
                }
            }
        }       
               
    }
}
