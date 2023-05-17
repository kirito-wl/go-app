pipeline {
    agent none
    stages {
        //DEV
        stage('Build Dev') {
            agent {
              label {
                label 'dev'
                customWorkspace "/home/osboxes/go-app"
              }
            }
            steps {
                sh 'git pull'
            }
        }
        stage('Test Dev') {
            agent {
                label {
                    label 'dev'
                    customWorkspace "/home/osboxes/go-app"
                }
            }
            steps {
                withEnv(["PATH=$PATH:/usr/local/go/bin", "CGO_ENABLED=1"]) {
                    // The Go command will now be available in the Jenkins pipeline.
                    sh 'go test ./...'
                }
            }
        }
        stage('Deploy Dev') {
            agent {
              label {
                label 'dev'
                customWorkspace "/home/osboxes/go-app"
              }
            }
            steps {
              script {
                withEnv ( ['JENKINS_NODE_COOKIE=do_not_kill'] ) {
                  sh 'go run main.go &'
                  }
                }
            }
        }

        //PROD
        stage('Build Prod') {
            agent {
              label {
                label 'production'
                customWorkspace "/home/osboxes/go-app"
              }
            }
            steps {
                sh 'git pull'
            }
        }
        stage('Test Production') {
            agent {
                label {
                    label 'production'
                    customWorkspace "/home/osboxes/go-app"
                }
            }
            steps {
                withEnv(["PATH=$PATH:/usr/local/go/bin", "CGO_ENABLED=1"]) {
                    // The Go command will now be available in the Jenkins pipeline.
                    sh 'go test ./...'
                }
            }
        }
        stage('Deploy Prod') {
            agent {
              label {
                label 'production'
                customWorkspace "/home/osboxes/go-app"
              }
            }
            steps {
              script {
                withEnv ( ['JENKINS_NODE_COOKIE=do_not_kill'] ) {
                  sh 'go run main.go &'
                  }
                }
            }
        }
        stage('Deploy Production Vue-App') {
            agent {
              label {
                label 'production'
                customWorkspace "/home/osboxes/vuejs-webapp-sample"
              }
            }
            steps {
              script {
                withEnv ( ['JENKINS_NODE_COOKIE=do_not_kill'] ) {
                  sh 'echo If this build is successful, app is accessible on ip:3000'
                  sh 'pm2 start npm --name "Test-App" -- run serve'
                  }
                }
            }
        }
    }
}
