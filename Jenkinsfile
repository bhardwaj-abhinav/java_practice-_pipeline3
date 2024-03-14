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
                       
                              bat '''
                               echo "Executing Unit Tests..."
                               mvn test
                              '''
                        
                  }
            }

            stage('Build'){
                  steps{
                        echo "Building version: ${VERSION} with suffix: ${RELEASE_VERSION}"
                        bat '''
                          
                          mvn versions:set -DnewVersion="${VERSION}"-SNAPSHOT
                          mvn versions:update-child-modules
                          mvn clean package
                        '''
                  }
            }
      }
}