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
        stage('Run production deployment') {
          when {
            branch 'main'
          }

          steps {
            build job: 'build_exam', parameters: [string(name: 'DEPLOY_TO', value: 'cloud')]
          }
    
        

        }
    }
}
