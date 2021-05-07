pipeline {
    agent any

    parameters{
        choice(choices: ['deploy.yml', 'destroy.yml'], description: "Action to perform", name: 'playbook')
        string(description: "Inventory to deploy against", name: "inventory", defaultValue: "docker-desktop.yml")
        password(description: "Vault Secret Key", name: "vault", defaultValue: "")
    }

    post {
        always {
            sh 'rm -rf *' // clean workspace 
            sh 'rm -rf .* || echo Done!' // clean hidden files, ignore errors
        }
    }

    stages {
        stage("Prepare Deployment"){
            steps {
                sh "rm -rf .ansible_vault"
                sh "set +x && [ ! -s ${params.vault} ] && echo ${params.vault} > .ansible_vault || echo 'No vault secret key provided!'"
                script {
                    secretProvided = fileExists(".ansible_vault")
                    if (secretProvided){
                        stage("Deploy"){
                            sh "ansible-playbook -i inventory/${params.inventory} -v ${params.playbook} --vault-password-file .ansible_vault"
                        }
                    }
                }
            }
        }
    }
}