pipeline {
    agent any
    environment {
        MIRROR_PATH             = '/mnt/los-mirror/LineageOS/android.git'
    }
    stages {
        stage('Preparation') {
            steps {
                echo 'Get Repo'
                sh 'mkdir -p ~/bin'
                sh 'curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo'
            }
        }
        stage('Repo Sync') {
            steps {
                dir("/mnt/los-mirror") {
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
