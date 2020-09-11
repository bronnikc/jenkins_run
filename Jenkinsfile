pipeline {
    agent any
	parameters
			{
			  string(name: 'ORACLE_HOME', defaultValue: 'db_home2', description: 'The target Oracle_HOME')
			}
	stages{

    stage('Start preparing with ansible-galaxy') {
	steps {
	  sh "ansible-galaxy install git+https://git.apps.okd.dcteam.local/oracle-ansible/install_oracle_home.git"
       ansiblePlaybook([
		playbook: "test.yml",
		inventory: "inventory",
		extraVars: [
					oracle_dbhome: ${params.ORACLE_HOME}
				   ]
		              ])
		}
    }
		}
}
