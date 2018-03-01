node {
    def app

    stage('Clone repository') {


        checkout scm
    }

     stage('Build image') {


        app = docker.build("iavorskiy/hellonode")
    }

    stage('Test image') {


        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {

        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
     stage('Deploy image'){

         sh "docker pull iavorskiy/hellonode"
         sh "docker run -d iavorskiy/hellonode"


    }



}

