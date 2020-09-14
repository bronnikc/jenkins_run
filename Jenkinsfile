pipeline {
    agent any
	parameters
			{
			  string(name: 'ORACLE_HOME', defaultValue: 'db_home1', description: 'The target Oracle_HOME')
			  string(name: 'HOST_ADDRESS', description: 'The target HOST IP')
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
			stage('Get ansible role from Git')
			{
			steps {
					sh "ansible-galaxy install git+https://git.apps.okd.dcteam.local/oracle-ansible/install_oracle_home.git"
			}
			}
			stage('Install ORACLE_HOME')
			{
				steps{
						ansiblePlaybook([
											playbook: "install_oracle_home.yml",
											extraVars: [
											oracle_dbhome: env.ORACLE_HOME,
											host_address: env.HOST_ADDRESS 
				   									   ]
		              					])
				}
			} 
		}
		}
	}
}
