def check_runs = new com.functions.buildGithubCheckScript()

pipeline {
   
    stages {
        stage('Checkout') {
            steps {
                script {
                    git (credentialsId: 'github-token',
                    url: "https://github.com/<organization-name>/" + repoName,
                    branch: "master")
                }
            }
        }
        stage("Build") {
            steps {
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: '<credentialsId>', keyFileVariable: 'privateKey', passphraseVariable: '', usernameVariable: '')]) {
                        try {
                            build_command = sh(script: "mvn clean install", returnStatus: true)
                            check_runs.buildGithubCheck(<REPO_NAME>, <COMMIT_ID>, privateKey, 'success', "build")
                        } catch(Exception e) {
                            check_runs.buildGithubCheck(<REPO_NAME>, <COMMIT_ID>, privateKey, 'failure', "build")
                            echo "Exception: ${e}"
                        }
                    }
                }
            }
        }
        stage("Unit Test") {
            steps {
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: '<credentialsId>', keyFileVariable: 'privateKey', passphraseVariable: '', usernameVariable: '')]) {
                        try {
                            def test = sh(script: "python unitTest.py", returnStdout: true)
                            check_runs.buildGithubCheck(<REPO_NAME>, <COMMIT_ID>, privateKey, 'success', "unit-test")
                        } catch(Exception e) {
                            check_runs.buildGithubCheck(<REPO_NAME>, <COMMIT_ID>, privateKey, 'failure', "unit-test")
                            echo "Exception: ${e}"
                        }
                    }
                }
            }
        }
        stage("Integration Test") {
            steps {
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: '<credentialsId>', keyFileVariable: 'privateKey', passphraseVariable: '', usernameVariable: '')]) {
                        try {
                            def test = sh(script: "python integrationTest.py", returnStdout: true)
                            check_runs.buildGithubCheck(<REPO_NAME>, <COMMIT_ID>, privateKey, 'success', "integration-test")
                        } catch(Exception e) {
                            check_runs.buildGithubCheck(<REPO_NAME>, <COMMIT_ID>, privateKey, 'failure', "integration-test")
                            echo "Exception: ${e}"
                        }
                    }
                }
            }
        }
    }
}
