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
                withAWS(region:'us-west-2',credentials:'aws') {
                    sh 'sudo aws eks --region us-west-2 update-kubeconfig --name udacity-project'                    
                }
            }
        }
        stage('Deploy Updated Image to Cluster'){
            steps {
                sh '''
                    export IMAGE="$registry:$BUILD_NUMBER"
                    sed -ie "s~IMAGE~$IMAGE~g" kubernetes/container.yml
                    sudo kubectl apply -f ./kubernetes
                    '''
            }
        }
     }
}