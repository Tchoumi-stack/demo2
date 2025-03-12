def gv

pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages {
        stage("building jar") {
            steps {
                sh "mvn package"
                    echo "building jar file"
                }
            }
        }
        stage("build docker image") {
            steps {
                sh "docker build -t myapp:1.0 ."
                    echo 'building docker image'
                }
            }
        } 
         stage("image tagging") {
            steps {
                sh "docker tag myapp:1.0 minelva/myapp:1.0"
                    echo 'building docker image'
                }
            }
      }
        stage("deploy image to dockerhub") {
            steps {
                script { 
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', passwordVariable: 'passwd', usernameVariable: 'username')]) {
    // some block {
                    sh "echo $passwd | docker login -u $username  --password-stdn"    
                    sh "docker push minelva/myapp:1.0"
                    echo "image deployed to dockerhub"
                } 
            }
        }
    }   
}
