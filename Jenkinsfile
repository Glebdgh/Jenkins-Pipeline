pipeline { 
    
    agent { label 'docker-slave-ssh' }
    
    stages { 
      stage('1-Clone') { 
             steps {
                sshagent(credentials: ['github-ssh']){
                 sh "ls -la"
                 sh "cd "
                 sh "git clone https://github.com/Glebdgh/Scripts.git"
                 sh "git checkout master"
                }
           }
        }
      stage('2-Build') { 
             steps {
               sh "chmod 777 build.sh" 
               sh "./build.sh" 
               sh "echo ${currentBuild.result} > artifact.txt"
            }
        }
      stage('3-Test') { 
             steps { 
               sh "chmod 777 test.sh" 
               sh "./test.sh" 
               sh "echo ${currentBuild.result} > test_result.txt"
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
