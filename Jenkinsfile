
pipeline  {
     agent  {label'slave1'}

    tools {
        
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                 sh 'git clone https://github.com/anilkumarpuli/dockerjenkins.git'
                 sh'rm -rf dockerjenkins'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
            stage('docker build')
            {
                steps{
                    sh'docker build -t anilkumblepuli/fisrtpipe:1.0.1 .'
                    sh'docker login -u anilkumblepuli -p Anilkumar@123'
                    sh'docker push anilkumblepuli/fisrtpipe:1.0.1 '
                    }
                    }
        }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.war'
                }
            }
        }
    




