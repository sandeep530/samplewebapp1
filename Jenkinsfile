pipeline {
agent 'any'

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    }

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush') 
{
    steps
    {
       sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ; sudo  docker login -usand3cs -pMrvsa@123 "
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ; sudo docker tag account-service sand3cs/account-service "
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ; sudo docker push sand3cs/account-service  "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node ( ' ansible-server '  ) {
             sh " sudo ansible-playbook /root/k8s.yaml"
   
    }
}
}
}
    
    
}
