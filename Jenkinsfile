pipeline { 
     agent { label 'docker-slave-ssh' } 
         
         stages { stage('1-Clone') { 
            steps { 
                  sh "ls -la;pwd" 
                  sh "git --version" 
                  sh "chmod 777 /home/jenkins" 
                  sh "git clone -b master https://github.com/Glebdgh/Scripts.git pr"
                  }
        }
      stage('2-Build') { 
            steps { 
               sh 'chmod -R +x pr' 
               sh 'pr/build.sh > artifact.txt'
             }
        }
      stage('3-Test') { 
          steps { 
             sh 'pr/test.sh > test_result.txt'
              }
          }
       }
        post { 
           always { 
             archiveArtifacts artifacts: 'artifact.txt'
        }
        failure { 
             archiveArtifacts artifacts: 'test_result.txt'
         }
       }
    }
