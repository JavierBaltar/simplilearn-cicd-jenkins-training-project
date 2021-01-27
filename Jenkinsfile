pipeline {
  agent none
  stages {
      
    stage("Git Checkout"){
        agent {
      label 'slave-01'
    }
            steps{
                echo "-----------------------------------------------------------------------------------------------------------------"
                echo "Git Checkout on Slave 01"
                echo "-----------------------------------------------------------------------------------------------------------------"
                git credentialsId: 'github', url: 'https://github.com/JavierBaltar/simplilearn-cicd-jenkins-training-project'
                
                
            }
        }  
  
  stage('Compile') {
    agent {
      label 'slave-01'
    }
    
    steps {
      echo "-----------------------------------------------------------------------------------------------------------------"
      echo "Compile on Slave 01"
      echo "-----------------------------------------------------------------------------------------------------------------"
                    
      sh 'mvn compile'
      
      
    }
  }
  
  stage('Test') {
    agent {
      label 'slave-02'
    }
    
    steps {
      echo "-----------------------------------------------------------------------------------------------------------------"
      echo "Testing on Slave 02"
      echo "-----------------------------------------------------------------------------------------------------------------"
      
      deleteDir()              
      unstash 'app'    
      sh "mvn test"
      junit '**/target/surefire-reports/*.xml'
      
    }
    
  }
  stage('Reports') {
    agent {
      label 'slave-02'
    }
    
    steps {
      echo "-----------------------------------------------------------------------------------------------------------------"
      echo "Reports on Slave 02"
      echo "-----------------------------------------------------------------------------------------------------------------"
      
      
    }
    post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
    
  }
}}
