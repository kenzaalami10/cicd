node {

    stage("Git Clone"){

        git credentialsId: 'kenzaalami10', url: 'https://github.com/kenzaalami10/cicd.git', branch: 'main' 
    }

     stage("Build") {

       sh 'docker build . -t meriemajaidi/node-todo-list:latest'
       sh 'docker image list'

    }

    withCredentials([string(credentialsId: 'meriemajaidi', variable: 'PASSWORD')]) {
        sh 'docker login -u meriemajaidi -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push meriemajaidi/node-todo-list:latest'
    }

    stage("kubernetes deployment"){
        sh 'kubectl apply -f deployment.yml'
    }
}
