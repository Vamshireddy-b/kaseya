pipeline{
    agent any;
    stages{
        stage('Initializing'){
            steps{
                println "Updating Host file with Given Credentials"
                script{
                hostInfo = "[win]\n"+VM_IP+"\n[win:vars]\nansible_user="+VM_Admin_User+"\nansible_password="+VM_Password+"\nansible_connection=winrm\nansible_winrm_server_cert_validation=ignore"
                }
                writeFile encoding: 'UTF-8', file: 'hosts', text: hostInfo
                println "Starting Update on the host $VM_IP with the user $VM_Admin_User"
            }
        }
        stage('Update Windows VM'){
            steps{
              ansiblePlaybook becomeUser: '$VM_Admin_User', colorized: true, installation: 'Ansible', inventory: 'hosts', playbook: 'windows_update.yml'
            }
        }
    }
}
