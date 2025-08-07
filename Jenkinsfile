pipeline {
    agent any

    tools {
        jdk 'jdk17'    
        maven 'Maven3' 
        nodejs 'NodeJS'
    }

    environment {
        SONARQUBE = 'sonarqube'
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_TOKEN = credentials('sonarqube')
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_IMAGE_PREFIX = 'houssemsouid'
    }

    stages {
        stage('Checkout Git repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Souid-Houssem/Microservice-App.git'
            }
        }




         stage('Build All Maven Projects') {
            steps {
                script {
                    // Find all directories containing a pom.xml
                    def pomDirs = sh(
                        script: "find . -name 'pom.xml' -exec dirname {} \\;",
                        returnStdout: true
                    ).trim().split("\n")

                    // Build each Maven project
                    pomDirs.each { dirPath ->
                        dir(dirPath) {
                            sh "mvn clean compile"
                        }
                    }
                }
            }
        }
           
        
        
        
        
        
        
   

        
       
        stage('Build Frontend (Angular)') {
            steps {
                echo "📦 Installing and Building Angular App"
                dir('Frontend') {
                    sh 'npm install'
                    sh 'npm run build -- --prod'
                }
            }
        }


        stage('Build Backend Images') {
            steps {
                // ✅ product-service (direct)
                dir('product-service') {
                    sh 'mvn clean package -DskipTests'
                    sh 'docker build -t $DOCKER_IMAGE_PREFIX/product-service:latest .'
                }

                // ✅ Billing-service (sous-dossier)
                dir('Billing-service/Billing-service') {
                    sh 'mvn clean package -DskipTests'
                    sh 'docker build -t $DOCKER_IMAGE_PREFIX/billing-service:latest .'
                }

                // ✅ eureka-service (sous-dossier)
                dir('eureka-service/eureka-service') {
                    sh 'mvn clean package -DskipTests'
                    sh 'docker build -t $DOCKER_IMAGE_PREFIX/eureka-service:latest .'
                }

                // ✅ gateway (sous-dossier)
                dir('gateway/gateway') {
                    sh 'mvn clean package -DskipTests'
                    sh 'docker build -t $DOCKER_IMAGE_PREFIX/gateway:latest .'
                }

                // ✅ Billing-producer ( 
                dir('Billing-producer') {
                    sh 'mvn clean package -DskipTests'
                    sh 'ls target' 
                    sh 'docker build -t $DOCKER_IMAGE_PREFIX/billing-producer:latest .'
                }

                // ✅ Analyse-Service (direct)
                dir('Analyse-Service') {
                    sh 'mvn clean package -DskipTests'
                    sh 'docker build -t $DOCKER_IMAGE_PREFIX/analyse-service:latest .'
                }

                // ✅ custmer-service (direct)
                dir('custmer-service') {
                    sh 'mvn clean package -DskipTests'
                    sh 'docker build -t $DOCKER_IMAGE_PREFIX/custmer-service:latest .'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('Frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'docker build -t $DOCKER_IMAGE_PREFIX/frontend:latest .'
                }
            }
        }

        stage('Push Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $DOCKER_IMAGE_PREFIX/product-service:latest'
                    sh 'docker push $DOCKER_IMAGE_PREFIX/billing-service:latest'
                    sh 'docker push $DOCKER_IMAGE_PREFIX/eureka-service:latest'
                    sh 'docker push $DOCKER_IMAGE_PREFIX/gateway:latest'
                    sh 'docker push $DOCKER_IMAGE_PREFIX/billing-producer:latest'
                    sh 'docker push $DOCKER_IMAGE_PREFIX/analyse-service:latest'
                    sh 'docker push $DOCKER_IMAGE_PREFIX/custmer-service:latest'
                    sh 'docker push $DOCKER_IMAGE_PREFIX/frontend:latest'
                }
            }
        }
                stage('Deploy Docker Stack') {
            steps {
                echo "🚀 Deploying docker-stack.yml to Docker Swarm"
                sh 'docker stack deploy -c docker-stack.yml microservices'
            }
        }

    }
}
