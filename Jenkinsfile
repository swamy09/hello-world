pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/swamy09/hello-world.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'webapp/target/*.war'
                }
            }
        }
        stage('Deploy'){
            steps {
                deploy adapters: [tomcat9(credentialsId: '7cfe2731-9af1-49a4-88ce-c6dbca1d9a17', path: '', url: 'http://3.86.108.0:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
