pipeline {
    agent any
    tools {
       ruby 'ruby-2.0.0p648'
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
        
        
            
        }
        stage('Copy artifact') {
            steps {
              copyArtifacts filter: 'main.rb', fingerprintArtifacts: true
            }
        }
        stage('Deliver') {
            steps {
              sshagent(['cloud']) {
                sh 'ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i cloud.ini playbook.yml'
             }
 
          }
        }
    }
