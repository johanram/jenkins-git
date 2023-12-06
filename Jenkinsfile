pipeline {
    agent {
        node {
            label 'ConjurServer'
        }
    }
    stages {
        stage('Install the cybr-cli') {
            steps {
                script {
                    def CONJUR_CLI_DOWNLOAD_URL = params.CONJUR_CLI_DOWNLOAD_URL
                    def CONJUR_CLI_FILE_NAME = params.CONJUR_CLI_FILE_NAME
                    sh "wget ${CONJUR_CLI_DOWNLOAD_URL}"
                    sh "tar -xzf ${CONJUR_CLI_FILE_NAME}"
                    sh "chmod +x cybr"
                }
                sh "./cybr version"
            }
        }
        stage('Authenticate with the cybr-cli') {
            steps {
                withCredentials([
                    conjurSecretCredential(credentialsId: 'CONJUR_ADMIN_USERNAME', variable: 'CONJUR_AUTHN_LOGIN'),
                    conjurSecretCredential(credentialsId: 'CONJUR_ADMIN_PASSWORD', variable: 'CONJUR_AUTHN_API_KEY')
                ]) {
                    script {
                        def CONJUR_APPLIANCE_URL = params.CONJUR_APPLIANCE_URL
                        def CONJUR_ACCOUNT = params.CONJUR_ACCOUNT
                        sh "./cybr conjur logon-non-interactive"
                    }
                }
            }
        }
        stage('Check Conjur authentication') {
            steps {
                withCredentials([
                    conjurSecretCredential(credentialsId: 'CONJUR_ADMIN_USERNAME', variable: 'CONJUR_AUTHN_LOGIN'),
                    conjurSecretCredential(credentialsId: 'CONJUR_ADMIN_PASSWORD', variable: 'CONJUR_AUTHN_API_KEY')
                ]) {
                    script {
                        sh "./cybr conjur whoami"
                    }
                }
            }
        }
        stage('List Conjur resources') {
            steps {
                withCredentials([
                    conjurSecretCredential(credentialsId: 'CONJUR_ADMIN_USERNAME', variable: 'CONJUR_AUTHN_LOGIN'),
                    conjurSecretCredential(credentialsId: 'CONJUR_ADMIN_PASSWORD', variable: 'CONJUR_AUTHN_API_KEY')
                ]) {
                    script {
                        sh "./cybr conjur list"
                    }
                }
            }
        }
    }
}
