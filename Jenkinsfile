pipeline {
    agent any

    environment {
        ABAP_REPO = 'https://github.com/srpsubbaraman/ABAP.git'
        REPO2 = 'https://github.com/srpsubbaraman/repo2.git'
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone ABAP') {
            steps {
                sh 'git clone $ABAP_REPO'
            }
        }

        stage('Push to repo2') {
            steps {
                dir('ABAP') {
                    withCredentials([usernamePassword(credentialsId: 'github-creds', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
                        sh '''
                            git remote add repo2 https://$GIT_USER:$GIT_PASS@github.com/srpsubbaraman/repo2.git
                            git push repo2 main
                        '''
                    }
                }
            }
        }
    }
}
