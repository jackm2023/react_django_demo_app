pipeline{
    agent {label 'dev'}
    stages{
        stage("Code Cloning"){
            steps{
                git url:'https://github.com/jackm2023/react_django_demo_app.git', branch:'master'
                echo "App Code cloned successfully"
            }
        }
        stage("App Build"){
            steps{
              sh 'docker build . -t jackmaseeh/react-app-todo:latest'
              echo "App Build successfully"
            }
        }
        stage("App Image Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerhubID',passwordVariable:'dockerHubpassword',usernameVariable:'dockerHubusername')]){
                    sh "docker login -u ${env.dockerHubusername} -p ${env.dockerHubpassword}"
                    sh "docker push jackmaseeh/react-app-todo:latest"
                }
            }
        }
        stage("App Deployed"){
            steps{
                sh 'docker-compose down && docker-compose up -d --no-deps --build myapp'
            }
        }
    }
}
