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
                sh 'sudo cp /var/lib/jenkins/workspace/pipeline/target/*.war /root/petwar'
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
        
        stage('jfrog'){
            
            steps{
                script{
                    def SERVER_ID = 'jfrog'
                    def server = Artifactory.server SERVER_ID
                    
                    def uploadSpec = """{
                        "files": [{
                                    "pattern": "**/*.war",
                                    "target": "pet"
                        }]
                    }"""
                    
                    server.upload(uploadSpec)
                }
            }
        }
    }
}
