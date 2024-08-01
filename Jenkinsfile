pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/BalaMadhavan2001/php-project.git/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t balamadhavan/sample:1.0 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push balamadhavan/sample:1.0'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 balamadhavan/sample:1.0'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.91.124 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.91.124 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
