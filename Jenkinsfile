pipeline {
   agent {label "kube-agent" }
   stages {
     stage('Git') {
         steps {
            git credentialsId: 'github_key', url: 'https://github.com/george-gta/jenkinsPipeline.git'
            
         }
    }
    stage('terraform') {
        steps{
           sh label: '', script: '''cd
pwd
rm -rf .ssh/known_hosts
ls -lthr /dev/tty
cd Terraform/hetzner
rm -rf ipterraformvm.txt
terraform destroy -auto-approve
terraform init
terraform apply -auto-approve
myvar=`cat ipterraformvm.txt`
echo $myvar
ssh -tt root@$myvar \'docker ps -a; exit\'
terraform destroy -auto-approve'''
}
}
}
}
}
