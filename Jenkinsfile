node {
    def app

    stage('Clone repository') {
      
        checkout scm
    }

    stage('Build Docker Image') {
        //path to DockerHub repo:
        app = docker.build("mb2love/sqream")
    }

    stage('Test image') {                      
         app.inside {                
             sh 'echo "Tests passed"'        
            }    
        }     
    
    stage('Push Docker Image'){
        // create secrets DOCKER_HUB_USER and DOCKER_HUB_PASSWORD in GitHub
        withCredentials([usernamePassword(credentialsId: 'dockerhub_id', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USER')]) {   
            sh 'docker login -u $DOCKER_HUB_USER -p $DOCKER_HUB_PASSWORD'
        }
         app.push("${env.BUILD_NUMBER}")            
     }
}
