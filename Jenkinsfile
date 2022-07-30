pipeline {
agent {
label 'buildserver'
}
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
        sh " sudo docker build -t webapps /home/ubuntu/workspace/dotnetapplication/app " 
    }
}   
     stage ('dockerimagepush')
{
    steps
    {
       sh "cd /home/ubuntu/workspace/dotnetapplication/app ;   sudo docker login -u sand3cs -p Mrvsa@123 "
        sh "cd /home/ubuntu/workspace/dotnetapplication/app ;  sudo docker tag webapps sand3cs/webapps "
        sh "cd /home/ubuntu/workspace/dotnetapplication/app ;  sudo docker push sand3cs/webapps  "

    }
}
       }
       }


