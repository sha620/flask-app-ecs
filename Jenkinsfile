pipeline {
    agent any;
    stages{
        stage(clone){
            steps{
                git url: "https://github.com/sha620/flask-app-ecs.git", branch: "main"
            }
        }
        stage(build){
            steps{
                sh " docker build -f ./Dockerfile-multi -t py:ll ."
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
                    credentialsId: "shakti",
                    usernameVariable: "user",
                    passwordVariable: "pass"
                    
                    )]) {
                        sh " docker login -u ${env.user} -p ${env.pass}"
                        sh " docker image tag py:ll ${env.user}/py:ll"
                        sh "docker push ${env.user}/py:ll"
                    }
            }
        }
        stage(deploy){
            steps{
                sh " docker run -d py:ll"
            }
        }
    }
}
