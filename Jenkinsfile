pipeline {
  agent any
     tools {
       maven 'M2_HOME'
           }
 
  stages {
    stage('Git Checkout') {
      steps {
        echo 'This stage is to clone the repo from github'
        git branch: 'master', url: 'https://github.com/ashakumar87/star-agile-health-care.git'
                        }
            }
    stage('Create Package') {
      steps {
        echo 'This stage will compile, test, package my application'
        sh 'mvn package'
                          }
            }
    stage('Generate Test Report') {
      steps {
        echo 'This stage generate Test report using TestNG'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Healthcare/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                          }
            }
    stage('Create Docker Image') {
      steps {
        echo 'This satge will create a docker image'
        sh 'docker build -t ashakumar893/healthcare:1.0 .'
                          }
            }
     stage('Login into dockerhub') {
      steps {
        echo 'This satge will loginto docker hub'
        withCredentials([usernamePassword(credentialsId: 'Dockerlogin', passwordVariable: 'dockerpass', usernameVariable: 'dockeruser')]) {
        sh 'docker login -u ${dockeruser} -p ${dockerpass}'
            }
      } 
     }
     stage('Docker Push-Image') {
      steps {
        echo 'This stage will push my new image to the dockerhub'
        sh 'docker push ashakumar893/healthcare:1.0'
            }
      }
   }
}
