pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                withEnv(["DOCKER_JENKINS_HOME=${env.DOCKER_JENKINS_MOUNT}"]) {
                    sh('''set +x ; source ./build-env.sh
                    build.sh''')
                }
            }
        }
        stage('Tests') {
            steps {
                sh('''set +x ; source ./build-env.sh
                go test''')
            }
        }
/*        stage('Deploy') {
            when { branch 'master' }
            steps {
                withCredentials([
                usernamePassword(credentialsId: 'github-jenkins-cred', usernameVariable: 'GITHUB_USER', passwordVariable: 'GITHUB_TOKEN')]) {
                    sh('''set +x ; source ./build-env.sh
                    publish.sh latest''')
                }
            }
        }*/
    }

    post {
        success {
            deleteDir()
        }
    }
}
