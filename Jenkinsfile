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
             sh " cd /var/lib/jenkins/workspace/sampleswebapp/app ; dotnet sonarscanner begin /k:"webapps" /d:sonar.host.url="http://ec2-54-147-53-22.compute-1.amazonaws.com:9000"  /d:sonar.login="2880cdefc52de9a2cb4b208ed0e9012b7add4e0c"
             sh " cd /var/lib/jenkins/workspace/sampleswebapp/app ; dotnet build"
             sh " cd /var/lib/jenkins/workspace/sampleswebapp/app ; dotnet sonarscanner end /d:sonar.login="2880cdefc52de9a2cb4b208ed0e9012b7add4e0c"
    }
}
}
}
    
    
}
