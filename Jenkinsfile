pipeline {
node {
        //cleanup current user docker credentials
        sh 'rm  ~/.dockercfg || true'
        sh 'rm ~/.docker/config.json || true'
        
        //configure registry
        docker.withRegistry('https://589197916977.dkr.ecr.us-east-1.amazonaws.com', 'ecr:eu-west-1:ad803b9c-11dc-43b2-9fad-c3548722f082') {
          
            //build image
            def customImage = docker.build("ecart-staging:${env.BUILD_ID}")
            
            //push image
            customImage.push()
        }
} 


}
