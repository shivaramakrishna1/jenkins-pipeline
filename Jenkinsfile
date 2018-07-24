pipeline {
    agent any
    
    stages{
        
        stage('git clone'){
            
            steps{
                git 'https://github.com/shivaramakrishna1/spring-petclinic.git'
            }
        }
        
        stage('Build'){
            
            steps{
                sh 'mvn clean install'
            }
        }
        
        stage('copy war to petwar dir'){
            
            steps{
                sh 'sudo cp /var/lib/jenkins/workspace/sample_test/target/*.war /root/petwar'
            }
        }
        
        stage('post build actions'){
            
            steps{
                archiveArtifacts 'target/petclinic.war'
            }
        }
        
        stage('JUnit test results'){
            
            steps{
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
}
