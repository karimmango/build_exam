pipeline {
    agent any
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
        stage('Deliver') {
            steps {
              sshagent(['cloud']) {
                sh 'ANSIBLE_HOST_KEY_CHECKING=False /usr/bin/ansible-playbook -i cloud.ini playbook.yml'
             }
 
          }
        }
    }
}
