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
    stage ('sonarqubetest')
    {    
    steps {
                script{
                    withSonarQubeEnv(credentialsId: 'sonarserver') {
                     sh "SonarScanner.MSBuild.exe begin /k:"webapps" /d:sonar.host.url="http://ec2-54-226-78-191.compute-1.amazonaws.com:9000" /d:sonar.login="3dfa85fd9e93e367944e279eac5e5a530075b365" " 
                     sh  " MsBuild.exe /t:Rebuild "
                     sh "   SonarScanner.MSBuild.exe end /d:sonar.login="3dfa85fd9e93e367944e279eac5e5a530075b365" "
                    }

                    timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                          
                        }
                    }

                }  
            }
        }
                          
    
       }
     }


