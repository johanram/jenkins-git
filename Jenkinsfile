pipeline {
    agent {
        node {
            label 'ConjurServer'
        }
    }
    stages {
        stage('Install cybr-cli') {
            steps {
                sh '''
                wget https://github.com/infamousjoeg/cybr-cli/releases/download/v1.0.1-release/cybr-cli_1.0.1-release_linux_amd64.tar.gz
                tar -xzf cybr-cli_1.0.1-release_linux_amd64.tar.gz
                chmod +x cybr
                '''
                sh './cybr version'
            }
        } 
        stage('Static Analysis') {
            steps {
                echo 'Run the static analysis to the code' 
            }
        }
        stage('Compile') {
            steps {
                echo 'Compile the source code' 
            }
        }
        stage('Security Check') {
            steps {
                echo 'Run the security check against the application' 
            }
        }
        stage('Run Unit Tests') {
            steps {
                echo 'Run unit tests from the source code' 
            }
        }
        stage('Run Integration Tests') {
            steps {
                echo 'Run only crucial integration tests from the source code' 
            }
        }
        stage('Publish Artifacts') {
            steps {
                echo 'Save the assemblies generated from the compilation' 
            }
        }
    }
}
