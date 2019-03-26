Skip to content
 
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@alfredogarza Sign out
 The password you provided is weak and can be easily guessed. To increase your security, please change your password as soon as possible.

Read our documentation on safer password practices.

1
0 633 alfredogarza/cicd-pipeline-train-schedule-dockerdeploy
forked from linuxacademy/cicd-pipeline-train-schedule-dockerdeploy
 Code  Pull requests 0  Projects 0  Wiki  Insights  Settings
cicd-pipeline-train-schedule-dockerdeploy/Jenkinsfile
@whboyd whboyd implement wait for feedback before Prod deploy
b71b9a6 on May 8, 2018
59 lines (59 sloc)  2.25 KB
    
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("willbla/train-schedule")
                    app.inside {
                        sh 'echo $(curl localhost:8080)'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_login') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
