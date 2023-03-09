pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    git branch: 'main', url: 'https://github.com/mohankumarsc/Demo-app.git'
                    
                    
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    def mavenHome =  tool name: "maven" , type: "maven"
                    def mavenCMD = "${mavenHome}/bin/mvn"
          
                    sh "${mavenCMD} test"
                    
                   '
                }
            }
        }
        
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    def mavenHome =  tool name: "maven" , type: "maven"
                    def mavenCMD = "${mavenHome}/bin/mvn"
          
                    sh "${mavenCMD} clean package"
                    
                   
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                    }
                }
            }
        }
        
}
