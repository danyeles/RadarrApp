pipeline {
    agent any

    environment {
        USERNAME = sh(script: 'echo $USER', returnStdout: true).trim()
        DOCKER_IMAGE = 'linuxserver/radarr:latest'
        CONTAINER_NAME = 'radarr'
        PUID = '1000'
        PGID = '1000'
        TZ = 'America/Monterrey'
        WEBUI_PORTS = '7878/tcp,7878/udp'
        CONFIG_PATH = '/home/docker/radarr/config'
    }

    stages {
        stage('Deploy Docker Image') {
            steps {
                script {
                    sh """                      
                    docker run -d \
                        --restart always \
                        --name ${CONTAINER_NAME} \
                        -p 8989:8989 \
                        -e PUID=${PUID} \
                        -e PGID=${PGID} \
                        -e TZ=${TZ} \
                        -v ${CONFIG_PATH}:/config \
                        -v /media/${USERNAME}/Media:/Media \
                        -v /media/${USERNAME}/Media/Downloads:/downloads \
                        -v /media/${USERNAME}/Media/Movies:/Movies \
                        -v /media/${USERNAME}/Media/MyMovies:/MyMovies \
                        ${DOCKER_IMAGE}
                    """
                }
            }
        }
    }
}
