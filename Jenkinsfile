pipeline {
    agent any
    parameters {
    choice choices: ['qa', 'cloud'], description: 'Select environment for deployment', name: 'DEPLOY_TO'
  }
    stages {
        stage('install requirements') {
            steps {
                sh 'gem install bundler -v1.17.3'
                
            }
          
            
        }
    
        stage('Save artifact') {
            steps {
              archiveArtifacts artifacts: 'main.rb', followSymlinks: false
                
            }
        }
        stage('Copy artifact') {
            steps {
              copyArtifacts filter: 'main.rb', fingerprintArtifacts: true,
                projectName: "build_exam", selector: lastSuccessful()
            }
        }
        stage('Deliver to cloud') {
            when {
                expression { params.DEPLOY_TO == 'cloud'}
            }
            steps {
              sshagent(['cloud']) {
                sh 'ANSIBLE_HOST_KEY_CHECKING=False /usr/bin/ansible-playbook -i ${DEPLOY_TO}.ini playbook.yml'
             }
 
          }
        }
        stage('Deliver to QA') {
            when {
                expression { params.DEPLOY_TO == 'qa'}
            }
            steps {
              sshagent(['vagrant-private-key']) {
                sh 'ANSIBLE_HOST_KEY_CHECKING=False /usr/bin/ansible-playbook -i ${DEPLOY_TO}.ini playbook.yml'
             }
 
          }
        }
    }
}
