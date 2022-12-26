pipeline {
    agent any
    tools{
        maven 'tien'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/NguyenTienHCL/automation-devops.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t tiennguyenhcl/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd1', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u tiennguyenhcl -p ${dockerhubpwd}'
                       

}
                   sh 'docker push tiennguyenhcl/devops-integration'
                }
            }
        }
    }
}
