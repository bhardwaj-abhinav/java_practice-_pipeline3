pipeline{
      agent any

      parameters{
            booleanParam(name: 'RELEASE', defaultValue: false, description: 'Is this a Release Candidate?')
      }

      environment {
            INT_VERSION = '0.1.0'
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
                 environment {
                        VERSION_SUFFIX = ${bat(script: 'if "%RELEASE%"=="false" (echo %INT_VERSION%ci:%BUILD_NUMBER%) else (echo %RELEASE_VERSION%ci:%BUILD_NUMBER%)', returnStdout: true)}
                  }

                  steps{
                        echo "Building version: ${INT_VERSION} with suffix: ${VERSION_SUFFIX}"
                        bat """
                          mvn versions:set -DnewVersion='${VERSION_SUFFIX}'-SNAPSHOT
                          mvn versions:update-child-modules
                          mvn clean package
                        """
                  }
            }


      }
}