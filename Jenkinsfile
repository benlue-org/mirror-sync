pipeline {
    agent any
    environment {
        MIRROR_PATH             = '/mnt/los-mirror/LineageOS/android.git'
    }
    stages {
        stage('Preparation') {
            steps {
                dir("${MIRROR_PATH}") {
                    sh '''#!/bin/bash
                       set -x
                       mkdir -p ~/bin
                       curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
                       source ~/.profile
                       repo init -u https://github.com/benlue-org/mirror --mirror                       
                    '''
                }
            }
        }
        stage('Repo Sync') {
            steps {
                dir("${MIRROR_PATH}") {
                    sh '''#!/bin/bash
                       set -x
                       source ~/.profile
                       repo sync -f --force-sync --force-broken --no-clone-bundle -j$(nproc --all)
                    '''
                }
            }
        }
    }
}
