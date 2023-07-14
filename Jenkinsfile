pipeline {
    agent any
    tools{
        maven 'maven_3_9_3'
    }
    
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/https-sysnet-ie/git_jenkins_integration.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t kernelsphere/kubernetes .'
                }
            }
        }
        stage('Push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'Murthy@123$', variable: 'Murthy@123$')]) {
                    sh 'docker login -u kernelsphere -p ${Murthy@123$}'
                        
                    }
                    sh 'docker push kernelsphere/kubernetes'
                }
            }
        }
        stage('Deploy to K8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'kubeconfig')
                }
            }
        }
    
    }    
}
