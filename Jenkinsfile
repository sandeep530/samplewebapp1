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
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app; sudo docker build -t webapps . " 
    }
}
     stage ('dockerimagepush') 
{
    steps
    {
       sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ; sudo  docker login -usand3cs -pMrvsa@123 "
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ; sudo docker tag webapps1 sand3cs/webapps "
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ; sudo docker push sand3cs/webapps "
        
        
    }
}
     
stage ('sonarqube') 
    {
        steps {
             sh " cd /var/lib/jenkins/workspace/sampleswebapp/app ; dotnet tool install --global dotnet-sonarscanner "
            
    }
}
}
}
    
    
}
