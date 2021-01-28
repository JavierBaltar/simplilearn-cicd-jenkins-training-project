pipeline {
  agent none
  environment {
        JUNIT_REPORTS_FOLDER = '**/target/surefire-reports/*.xml'
  }
  stages {
      stage('Compile') {
          agent {
              label 'slave-01' /* this stage executor and workspace is allocated in slave-01 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Compile on Slave 01 "
              echo "-----------------------------------------------------------------------------------------------------------------"
              sh 'mvn compile' /* compile source code */
          }
      }
      stage('Test') {
          agent {
              label 'slave-02' /* this stage executor and workspace is allocated in slave-02 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Testing on Slave 02"
              echo "-----------------------------------------------------------------------------------------------------------------"
              sh 'mvn test' /* test the compiled source code using unit testing framework */
              junit '${JUNIT_REPORTS_FOLDER}'
          }
      }
      stage('Reports') {
          agent {
              label 'slave-02' /* this stage executor and workspace is allocated in slave-02 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Reports on Slave 02"
              echo "-----------------------------------------------------------------------------------------------------------------"
          }
          post {
              always {
                  junit '**/target/surefire-reports/*.xml' /* publish unit testing reports */
                  deleteDir() /* workspace clean up */
              }
          }
      }
   }
}
