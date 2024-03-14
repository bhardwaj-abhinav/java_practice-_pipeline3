pipeline{
      agent any

      environment {
            VERSION = '0.1.0'
            RELEASE_VERSION = 'R.2'
      }

      stages {
            stage('Audit tools'){
                  steps {
                        bat '''
                           git --version
                           java --version
                           mvn --version   
                        '''
                  }
            }

            stage('Unit Test') {
                  steps{
                        dir('/'){
                              bat '''
                               echo "Executing Unit Tests..."
                               mvn test
                              '''
                        }
                  }
            }

            stage('Build'){
                  steps{
                        bat '''
                          echo "Building version: ${VERSION} with suffix: ${RELEASE_VERSION}"
                          mvn -f javaapp_pipeline/pom.xml clean install
                        '''
                  }
            }
      }
}