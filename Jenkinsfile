pipeline {
    agent any

    stages {
        stage('Build') {
            parallel {
                stage('Build Frontend') {
                    agent {
                        docker {
                            image 'node:14'
                        }
                    }
                    steps {
                        script {
                            dir('frontend') {
                                sh 'docker build -t myapp-frontend .'
                            }
                        }
                    }
                }
                stage('Build Backend') {
                    agent {
                        docker {
                            image 'node:14'
                        }
                    }
                    steps {
                        script {
                            dir('backend') {
                                sh 'docker build -t myapp-backend .'
                            }
                        }
                    }
                }
                stage('Build Database') {
                    agent {
                        docker {
                            image 'mysql:5.7'
                        }
                    }
                    steps {
                        script {
                            dir('database') {
                                sh 'docker build -t myapp-database .'
                            }
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.compose.up '-d'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
