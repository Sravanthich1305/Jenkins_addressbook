pipeline {
        agent {
            label 'master'
        }
        tools {
            maven 'maven3.6.3'
            jdk 'jdk11'
        }
    stages {

        stage ('Checkout the code') {
            steps{
                git branch: 'main', url: 'https://github.com/Sravanthich1305/Jenkins_addressbook.git'
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
