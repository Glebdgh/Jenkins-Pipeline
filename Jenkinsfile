pipeline { 
     agent { label 'docker-slave-ssh' } 
         
         stages { stage('1-Clone') { 
            steps { 
                  sh "ls -la;pwd" 
                  sh "git --version" 
                  sh "chmod 777 /home/jenkins" 
                  sh "git clone -b $ghprbSourceBranch https://github.com/Glebdgh/Scripts.git"
                  }
        }
      stage('2-Build') { 
            steps { 
               sh "cd Scripts"
               sh 'chmod -R +x Scripts' 
               sh 'Scripts/build.sh > artifact.txt'
             }
        }
      stage('3-Test') { 
          steps { 
             sh 'Scripts/test.sh > test_result.txt'
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
