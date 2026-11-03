pipeline {
    agent any

    stages {
        stage("checkout"){
            steps{
                echo "checkout"
                git branch: 'main', credentialsId: 'omarrabh', url: 'https://github.com/Omar-Rabh/devops-study-depi.git'
                sh 'ls'
            }
        }
        stage("build"){
            steps{
                sh 'docker build . -t omarrabh54/firt-app-v2'
            }
        }
        stage("test"){
            steps{
                sh 'docker run -d omarrabh54/firt-app-v2 echo "testing...."'
            }
        }
        stage("Release"){
            steps{
               // docker login username & password wmn mkany haza a7b awgeh kol elshokr lbashmohands abobakr ❤️❤️
               withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'dockerPass', usernameVariable: 'dockerUser')]) {
               sh '''
               set +x
               printf '%s' "$dockerPass" | docker login -u $dockerUser --password-stdin
               docker push omarrabh54/firt-app-v2
               '''
                }
            }
        }
        stage("Deploy"){
            steps{
                input cancel: 'no', message: 'Continue for deployment ?!', ok: 'Deploy'
                //run a container from the image u just created 
                sh 'docker run -d omarrabh54/firt-app-v2 sleep 1d'
            }
        }
    }
}
