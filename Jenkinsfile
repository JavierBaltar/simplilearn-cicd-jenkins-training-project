pipeline {
  agent none
  environment {
      JUNIT_REPORTS_FOLDER = "**/target/surefire-reports/*.xml" /* set junit reports folder variable */
  }
  options {
      skipDefaultCheckout true /* skips the default repository checkout for testing the 'stash/unstash' feature behaviour */
  }
  stages {
      stage('Checkout code by slave-01') {
          agent {
              label 'slave-01' /* this stage executor and workspace is allocated in slave-01 node */
          }  
          steps {
            checkout scm /* checkout source repository */
            stash includes: '**', name: 'repository_code' /* stores code to be handed over to slave-02 */
          }
      }
      stage('Maven compile by slave-01') {
          agent {
              label 'slave-01' /* this stage executor and workspace is allocated in slave-01 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Maven Compile by Slave 01"
              echo "-----------------------------------------------------------------------------------------------------------------"
              sh 'mvn compile' /* compile source code */
          }
          post {
              always {
                  deleteDir() /* workspace clean up */
              }
          }
      }  
      stage('Maven testing by slave-02') {
          agent {
              label 'slave-02' /* this stage executor and workspace is allocated in slave-02 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Maven Application Testing by Slave 02"
              echo "-----------------------------------------------------------------------------------------------------------------"
              unstash 'repository_code' /* retrieves code stored by slave-01 */
              sh 'mvn test' /* test the compiled source code using unit testing framework */
          }
      }
      stage('Publish testing reports by slave-02') {
          agent {
              label 'slave-02' /* this stage executor and workspace is allocated in slave-02 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Publish Testing Reports by Slave 02"
              echo "-----------------------------------------------------------------------------------------------------------------"
          }
          post {
              always {
                  junit "${JUNIT_REPORTS_FOLDER}" /* publish unit testing reports */
                  deleteDir() /* workspace clean up */
              }
          }
      }
   }
}
