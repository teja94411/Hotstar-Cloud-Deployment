pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-container-hub-cred'
        DOCKER_IMAGE_NAME = 'tejaroyal/hotstar:latest'
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout from Git') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'githu-token', url: 'https://github.com/teja94411/Hotstar-Cloud-Deployment.git']])
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    if (isUnix()) {
                        sh "npm install"
                    } else {
                        bat "npm install"
                    }
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: DOCKER_CREDENTIALS_ID,
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )]) {
                        if (isUnix()) {
                            sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                        } else {
                            bat '''
                                echo %DOCKER_PASS% > pass.txt
                                docker login -u %DOCKER_USER% --password-stdin < pass.txt
                                del pass.txt
                            '''
                        }
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    if (isUnix()) {
                        sh "docker build -t hotstar ."
                        sh "docker tag hotstar $DOCKER_IMAGE_NAME"
                        sh "docker push $DOCKER_IMAGE_NAME"
                    } else {
                        bat "docker build -t hotstar ."
                        bat "docker tag hotstar %DOCKER_IMAGE_NAME%"
                        bat "docker push %DOCKER_IMAGE_NAME%"
                    }
                }
            }
            stage('Deploy to container') {
                 steps {
                   script {
                      if (isUnix()) {
                          // For Linux/MacOS
                     sh 'docker run -d --name hotstar -p 3000:3000 tejaroyal/hotstar:latest'
                    } else {
                        // For Windows
                     bat 'docker run -d --name hotstar -p 3000:3000 tejaroyal/hotstar:latest'
               }
           }
       }
     }
        }
    }
}
