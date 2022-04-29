pipeline {
    agent any
    parameters {
    choice choices: ['qa', 'production','staging', 'cloud'], description: 'Select environment for deployment', name: 'DEPLOY_TO'
    string(name: 'upstreamJobName',
          defaultValue: 'main',
          description: 'The name of the job the triggering upstream build'
    )
  }
    tools {
       go 'go-1.17.8'
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
//         stage('run qa deploy') {
//             when{
//                 not {
//                     branch 'main'
//                 }
//             }
            
//         steps {
//             build job: 'build_exam', parameters: [string(name: 'DEPLOY_TO', value: 'qa'),
//                                                  string(name: 'upstreamJobName', value: 'main')]
//         }
        
        
            
        //}
        stage('Run production deployment') {
          when {
            branch 'main'
          }

          steps {
            build job: 'build_exam', parameters: [string(name: 'DEPLOY_TO', value: 'cloud'),
                                                     string(name: 'upstreamJobName', value: BRANCH_NAME)]
          }
    
        

        }
    }
}
