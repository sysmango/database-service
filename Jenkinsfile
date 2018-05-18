pipeline {
      agent { label 'espresso' } 

      stages{
            /* tests for ansible scripts */
            /* YAML linter */
            stage('Yaml Validation') {
                steps{ 
                  //run yamllint parameter required is the path where the playbooks are stored
                  script {
                      parallel(
                              a: {
                                    try{
                                          sh "yamllint -c jenkins/yamllint_config *.yml"
                                    } catch (err) {
                                          echo "yamllint reported errors, continuing with pipeline"
                                          currentBuild.result = 'UNSTABLE' 
					      }                                          
                              },
                              b: {
                                    try{
                                          sh "yamllint -c jenkins/yamllint_config */*.yml"
                                    } catch (err) {
                                          echo "yamllint reported errors, continuing with pipeline"
                                          currentBuild.result = 'UNSTABLE'
					      }
                              },
                              )
                        }                  
                 }
            }
            stage('Ansible Lint') {
                                steps{ 
                  //run ansible-lint parameter required is the path where the playbooks are stored
                  script {
                      parallel(
                              a: {
                                    try{
                                          sh "ansible-lint -c jenkins/ansible-lint_config *.yml"
                                    } catch (err) {
                                          echo "ansible-lint reported errors, continuing with pipeline"
                                          currentBuild.result = 'UNSTABLE' 
					      }                                          
                              },
                              b: {
                                    try{
                                          sh "ansible-lint -c jenkins/ansible-lint_config */*.yml"
                                    } catch (err) {
                                          echo "ansible-lint reported errors, continuing with pipeline"
                                          currentBuild.result = 'UNSTABLE'
					      }
                              },                             
                       )
                  }                  
            }
      }
      // }
	// }
            /* Commented out this stage because syntax check is already done by ansible-lint
            stage('Ansible Playbook Syntax Check') {
                steps{
                  script {                        
                        //running ansible playbook syntax checker"
                        parallel(
                              a: {                        
                                    sh ""//"ansible-playbook --syntax-check *.yml" 
                              },
                              b: {                                    
                                    sh ""//"ansible-playbook --syntax-check group_vars/*.yml" 
                              },
                              c: {                                    
                                    sh ""//"ansible-playbook --syntax-check roles/7zipinstall/tasks/*.yml"
                              },
                              d: {                                    
                                    sh ""//"ansible-playbook --syntax-check roles/HypCreateUsers/tasks/*.yml"
                              },
                              e: {                                    
                                    sh ""//"ansible-playbook --syntax-check roles/IISInstall/tasks/*.yml"
                              },
                              f: {                                    
                                    sh ""//"ansible-playbook --syntax-check roles/HypRegistry_tcpparam/tasks/*.yml"
                              },
                              g: {                                    
                                    sh ""//"ansible-playbook --syntax-check roles/SetPowerPerf/tasks/*.yml"
                              },
                              h: {                                    
                                    sh ""//"ansible-playbook --syntax-check roles/UACDisable/tasks/*.yml"
                              },
                              i: {                                    
                                    sh ""//"ansible-playbook --syntax-check roles/VCinstall/tasks/*.yml"   
                              }
                        )
                  }
                }
            }*/
            /* Commented out this stage because check will not work without connectivity to endpoints
            stage('Ansible Playbook Dry Run') {
                steps{
                  script {  
                        parallel(
                              a: {                        
                                    //running ansible playbook dry run checker"
                                    sh ""//"ansible-playbook --check *.yml"
                              },
                              b: {                                    
                                    sh ""//"ansible-playbook --check group_vars/*.yml"
                              },
                              c: {                                    
                                    sh ""//"ansible-playbook --check roles/7zipinstall/tasks/*.yml"
                              },
                              d: {                                    
                                    sh ""//"ansible-playbook --check roles/HypCreateUsers/tasks/*.yml"
                              },
                              e: {                                    
                                    sh ""//"ansible-playbook --check roles/IISInstall/tasks/*.yml"
                              },
                              f: {                                    
                                    sh ""//"ansible-playbook --check roles/HypRegistry_tcpparam/tasks/*.yml"
                              },
                              g: {                                    
                                    sh ""//"ansible-playbook --check roles/SetPowerPerf/tasks/*.yml"
                              },
                              h: {                                    
                                    sh ""//"ansible-playbook --check roles/UACDisable/tasks/*.yml"
                              },
                              i: {                                    
                                    sh ""//"ansible-playbook --check roles/VCinstall/tasks/*.yml"  
                              }                                   
                        )
                  }                  
                }
            }*/
            stage('Ansible Playbook Analytics Logged') {
                steps{
                  script {
                        //running grep to ensure all ansible playbooks are writing logs analytics team needs"
                        // currently on searching root if want to search all files use **/*.yml
                        def filesToProcess = findFiles(glob: '**.yml')
                        for (def fileToProcess : filesToProcess) {
                              //sh "echo grep hosts ${fileToProcess}"
                              echo "grep hosts ${fileToProcess}"
                        }
                  }                  
                }
            }
      }
      post { 
        unstable { 
            echo 'Todo send a message to slack when pipeline is unstable!'
        }
        failure { 
            echo 'Todo send a message to slack when pipeline fails!'
        }
        always { 
            echo 'Thank you I have been your Jenkins pipeline today, as a worker in the service industry any and all gratuities are welcome!'
        }
    }
}


