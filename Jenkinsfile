pipeline {
        agent {
            label 'master'
        }
        tools {
            maven 'mymaven'
            jdk 'myjava'
        }
    stages {

        stage ('Checkout the code') {
            steps{
                git branch: 'main', url: 'https://git@github.com:devopstrainers1/addressbook.git'
            }
        }

      stage ('Parallel block') {
       parallel {   
        stage ('Code Validate') {
            steps{
                sh """
                mvn validate
                """
            
        }
        }

        stage ('Code Compile') {
            steps{
               
                sh """
                mvn compile
                """
            
        }
        }
       }
      }

        stage ('JUNIT Test') {
            steps{
                sh """
                mvn test
                """
            }
        }

        stage ('Packaging') {
            steps {
                sh """
                mvn package
                """

            }
        }


      }
      post {

          always{
              junit 'target/surefire-reports/**/*.xml'
          }
      }   

}
