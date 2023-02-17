pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/AfridBashaM/simple-java-app.git'
                }
            }
        }
        
        stage('SCA'){
            
            steps{
                
                script{
                    
                    dependencyCheck additionalArguments: '', odcInstallation: 'owasp dependency'
                }
                                             
            }
           
        }
        
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('SAST'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                 }
             }
         }
         stage ('Deploy-To-Tomcat') {
             
            steps {
                
              deploy adapters: [tomcat9(path: '', url: 'http://52.66.142.113:8080/')], contextPath: '/prod/apache-tomcat-9.0.71/webapps/simple-java-app', war: '**/*.war'      
              }       
            }
        }
    }     
}
