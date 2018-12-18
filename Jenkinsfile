pipeline {
    agent any

    stages {
        stage('Checkout') {
            checkout scm
        }
        stage('Load Plugins') {
            steps {
                sh "gem install octopress-minify-html"
            }
        }
        stage('Build') {
            steps {
                script {
                    if (env.BRANCH_NAME.equals("master")) {
                        sh "jekyll build --incremental"
                    } else {
                        sh "jekyll build --incremental --drafts"
                    }
                }
            }
        }
    }

    post {
        success {
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '_site', reportFiles: 'index.html', reportTitles: ''])
            archiveArtifacts artifacts: 'jenkins-jekyll/', fingerprint: true, onlyIfSuccessful: true
            }
    }
}
