pipeline {
  agent none
  
  stages {
      stage('Maven Compile by Slave 01') {
          agent {
              label 'slave-01' /* this stage executor and workspace is allocated in slave-01 node */
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Maven Compile by Slave 01"
              echo "-----------------------------------------------------------------------------------------------------------------"
              sh 'mvn compile' /* compile source code */
          }
      }
      stage('Maven Application Testing by Slave 02') {
          agent {
              label 'slave-02' /* this stage executor and workspace is allocated in slave-02 node */
          }
          environment {
              JUNIT_REPORTS_FOLDER = "**/target/surefire-reports/*.xml"
          }
          steps {
              echo "-----------------------------------------------------------------------------------------------------------------"
              echo "Maven Application Testing by Slave 02"
              echo "-----------------------------------------------------------------------------------------------------------------"
              sh 'mvn test' /* test the compiled source code using unit testing framework */
              junit "${JUNIT_REPORTS_FOLDER}"
          }
      }
      stage('Publish Testing Reports by Slave 02') {
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
                  junit '**/target/surefire-reports/*.xml' /* publish unit testing reports */
                  deleteDir() /* workspace clean up */
              }
          }
      }
   }
}
