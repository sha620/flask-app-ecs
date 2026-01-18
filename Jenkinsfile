pipeline {
    agent any;
    stages(){
        stage(clone){
            steps{
                git url: "https://github.com/sha620/flask-app-ecs", branch: "main"
            }
        }
        stage(build){
            steps{
                sh "docker build -f ./Dockerfile-multi -t py-app:ll ."
            }
        }
        stage(test){
            steps{
                echo "test"
            }
        }
        stage(push){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "new",
                    usernameVariable: "user",
                    passwordVariable: "pass"
                    )]){
                        sh "docker login -u ${env.user} -p ${env.pass}"
                        sh "docker image tag py-app:ll ${env.user}/py-app:ll"
                        sh "docker push ${env.user}/py-app:ll"
                    }
            }
        }
        stage(deply){
            steps{
                sh "docker run -d py-app:ll"
            }
        }
    }
}
