pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'linuxserver/radarr:latest'
        CONTAINER_NAME = 'radarr'
        PUID = '1000'
        PGID = '1000'
        TZ = 'America/Monterrey'
        WEBUI_PORTS = '7878/tcp,7878/udp'
        CONFIG_PATH = '/home/docker/radarr/config'
        MEDIA_PATH = '/mnt/Media'
        MOVIES_PATH = '/mnt/Media/Movies'
        MYMOVIES_PATH = '/mnt/Media/MyMovies'
        DOWNLOADS_PATH = '/mnt/Media/Downloads'
        MVSDOWNLOADS_PATH = '/mnt/Media/Movies/MoviesDownloads'
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
                        -v ${MEDIA_PATH}:/Media \
                        -v ${DOWNLOADS_PATH}:/downloads \
                        -v ${MOVIES_PATH}:/Movies \
                        -v ${MYMOVIES_PATH}:/MyMovies \
                        -v ${MVSDOWNLOADS_PATH}:/MoviesDownloads \
                        ${DOCKER_IMAGE}
                    """
                }
            }
        }
    }
}
