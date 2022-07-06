# devops

#Install docker and docker-compose
apt-get remove docker docker-engine docker.io containerd runc

apt-get update -y


####################
apt-get install ca-certificates curl  gnupg lsb-release -y

mkdir -p /etc/apt/keyrings

 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg


 ###################################
 echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


 apt-get update


 apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin



 #Install terrafrom


 apt-get update && sudo apt-get install -y gnupg software-properties-common curl

 curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -


 sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"


 //stages {
        stage("Run AWS thing part 1") {
            steps {
                withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding', 
                        credentialsId: 'aws_id', 
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'      
                ]]) {
                    sh "aws sts get-caller-identity"
            }
        }