#!groovy

pipeline {
  
  agent any
  stages {
   
        stage('Test slave-01') {
        steps{
            node('slave-01') {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Starting Test on Slave 01"
              echo "-----------------------------------------------------------------------------------------------------------------"
              sh ("hostname")
            }
        }
        }
    
        stage('Cleanup Workspace') {
            steps {
              node('slave-01') {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Starting Test on Slave 01"
              echo "-----------------------------------------------------------------------------------------------------------------"
              cleanWs()
              sh """
                echo "Cleaned Up Workspace for Application"
                """
              }
        }
        }
    
        stage('Test slave-02') {
        steps{
            node('slave-02') {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Starting Test on Slave 02"
              echo "-----------------------------------------------------------------------------------------------------------------"
              sh ("hostname")
            }
        }
        }

        
    

       
    
       
       
    
   }   
}
