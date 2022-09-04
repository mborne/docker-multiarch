pipeline {
    agent { label 'docker' }

    environment {
        DOCKER_REGISTRY_URL = 'https://registry.quadtreeworld.net'
        DOCKER_REGISTRY_CREDENTIAL_ID = 'nexus_user'
        DOCKER_PLATFORMS = "linux/arm/v7,linux/arm64/v8,linux/amd64"
    }

    stages {
        stage('MultiArch build') {
            steps {
                script {
                    sh 'docker buildx create builder --use'
                    docker.withRegistry("${DOCKER_REGISTRY_URL}", "${DOCKER_REGISTRY_CREDENTIAL_ID}") {
                        sh "docker buildx build --push --platform ${DOCKER_PLATFORMS} --tag registry.quadtreeworld.net/multiarch:latest ."
                    }
                }
            }
        }
    }
}