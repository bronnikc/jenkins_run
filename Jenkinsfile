pipeline {
    agent any
	parameters
			{
			  string(name: 'ORACLE_HOME', defaultValue: 'db_home2', description: 'The target Oracle_HOME')
			}
	stages{
		stage('Read Jenkinsfile') {
            when {
                expression { return params.refresh_configure == true }
            }
            steps {
              echo("Reread config")  
            }
        }
    stage('Start run playbook') 
		{
			when {
				 expression { return params.refresh_configure == false }
			}	
		stages{
			stage('Get From Git')
			{
			steps {
					sh "ansible-galaxy install git+https://git.apps.okd.dcteam.local/oracle-ansible/install_oracle_home.git"
			}
			}
			stage('Run playbook')
			{
				steps{
						ansiblePlaybook([
											playbook: "test.yml",
											inventory: "inventory",
											extraVars: [
											oracle_dbhome: env.ORACLE_HOME
				   									   ]
		              					])
				}
			} 
		}
		}
	}
}
