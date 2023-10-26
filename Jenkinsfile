pipeline{
    agent{
        node{
            label('workstation')
        }
    }

    parameters{
    string(name: 'COMPONENT', defaultValue:'', description:'Which Component')
    string(name: 'ENV', defaultValue:'', description:'Which Env')
    string(name: 'APP_VERSION', defaultValue:'', description:'Which Version')
    }

    stages{

        stage ('Get Servers'){
            steps{
            sh 'aws ec2 describe-instances  --filters "Name=tag:Name,Values=${COMPONENT}-${env}" --query "Reservations[*].Instances[*].PrivateIpAddress" --output text > inv'
            }
        }

        stage('Deploy Application'){
            steps{
            sh 'ansible-playbook -i inv main.yml -e ansible_user=centos -e ansible_password=DevOps321 -e app_version=${APP_VERSION} -e role_name=${COMPONENT} -e env=${ENV}'
            }
        }
    }

}