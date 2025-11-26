pipeline{
    agent any;
    stages{
        stage(clone){
            steps{
                git url: "https://github.com/sha620/flask-app-ecs.git", branch: "main"
            }
        }
        stage(build){
            steps{
                sh "docker build -f ./Dockerfile-multi -t app:ll ."

            }
        }
        stage(test){
            steps{
                echo "test"
            }
        }
        stage(push){
            steps{
                echo "push"
            }
        }
        stage(deploy){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "singh",
                    usernameVariable: "user",
                    passwordVariable: "pass"
                    )]){
                        sh "docker login -u ${env.user} -p ${env.pass}"
                        sh "docker image tag app:ll ${env.user}/app:ll"
                        sh "docker push ${env.user}/app:ll"
                    }
            }
        }
    }
    
}
