pipeline {
       agent {
        node {
            label 'jenkins-slave-node'
        }
    }
   
    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"               
    }
    stages {
        stage("build stage"){
            steps {
                echo "----------- build started -----------"
                sh 'mvn clean package -Dmaven.test.skip=true'
                echo "----------- build completed -------------"
            }
        }
      
        stage("test stage"){
            steps{
                echo "----------- unit test started -----------"
                sh 'mvn surefire-report:report'
                echo "----------- unit test Completed ----------"
            }
        }

         stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sonar-scanner-cofigure'
            }
            steps{
                withSonarQubeEnv('sonar-server-configure') {
                    sh "${scannerHome -X}/bin/sonar-scanner"
                }
            }
        }
    }
}









