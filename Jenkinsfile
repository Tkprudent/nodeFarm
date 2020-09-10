pipeline {
     agent any
     environment {
        registry = "ktijani/udacity-capstone"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
     stages {
         stage('Lint files') {
              steps {
                  sh 'make lint'
              }
         }
         stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Upload Image to Docker hub') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
        stage('Update Kube Config'){
            steps {
                withAWS(region:'us-east-1',credentials:'udacity-cloudDevops-capstone') {
                    sh 'sudo aws eks --region us-east-1 update-kubeconfig --name udacity-cloudDevops'                    
                }
            }
        }
        stage('Deploy Updated Image to Cluster'){
            steps {
                sh '''
                    export IMAGE="$registry:$BUILD_NUMBER"
                    sed -ie "s~IMAGE~$IMAGE~g" kubernetes-resources/deployment.yml
                    sudo kubectl apply -f ./kubernetes-resources
                    '''
            }
        }
     }
}