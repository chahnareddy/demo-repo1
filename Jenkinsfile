pipeline {
    agent any
    environment {
       // DOCKERHUB_CREDENTIALS = credentials('dockerhub')
       dockerImage=''
       registry= "sukanyapoli/newimage"
       registryCredential= 'dockerhub'
    }
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven1"
        jdk  "java1"
    }

    stages {
        stage("git") {
            steps {
                
                git credentialsId: 'git', url: 'https://github.com/chahnareddy/addressbook.git'
               sh "mvn compile"
            
            }

        }
        
        stage("Package") {
            steps {
                
                script{
                sh "mvn package"
            
                }
                
            }

        }
        stage("Docker build") {
            steps {
                
                script{
               // sh "docker build -t sukanyapoli/images:$BUILD_NUMBER ."
               dockerImage= docker.build registry
            
                }
                
            }

        }
        stage("Docker push") {
            steps {
                
                script{
               
                docker.withRegistry('',registryCredential ){
                    dockerImage.push()
                }
            
                }
                
            }

        }
    }
    
    post {
        
      always {
        junit '**/surefire-reports/*.xml'
      }
    } 
        
    }
