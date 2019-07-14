node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "hello-kenzan"
    registryHost = "127.0.0.1:30400/"
    imageName = "${registryHost}${appName}:${tag}"
    env.BUILDIMG=imageName

    stage "Build"
    
        sh "docker build -t rajivkumarhp/test1:latest -f applications/hello-kenzan/Dockerfile applications/hello-kenzan"
    
    stage "Push"
withDockerRegistry([credentialsId: 'regcreds', url: 'https://hub.docker.com']) 
    {
        sh "docker push rajivkumarhp/test1:latest"
    } 
   // stage "Deploy"

     //   kubernetesDeploy configs: "applications/${appName}/k8s/*.yaml", kubeconfigId: 'kenzan_kubeconfig'

}
