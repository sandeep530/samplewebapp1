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
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ;  docker build -t webapps . "
    }
}
     stage ('dockerimagepush')
{
    steps
    {
       sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ;   docker login -usand3cs -pMrvsa@123 "
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ;  docker tag account-service sand3cs/account-service "
        sh "cd /var/lib/jenkins/workspace/sampleswebapp/app ;  docker push sand3cs/account-service  "

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
