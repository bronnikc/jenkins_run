ipeline {
    agent any
	parameters
			{
			  string(name: 'ORACLE_HOME', defaultValue: 'dbhome_1', description: 'The target Oracle_HOME')
			  string(name: 'HOST_ADDRESS', defaultValue: '192.168.1.229', description: 'The target HOST IP')
			   string(name: 'ORACLE_DB_NAME', defaultValue: 'orcl', description: 'Oracle database name')
			  choice(choices: 'no_archivelog\narchivelog', description:'ARCHIVELOG_MODE', name: 'ARCHIVELOG_MODE')
			  string(name: 'DB_CREATE_FILE_DIST', defaultValue: 'default',description: 'destination for dbfiles')
			  string(name: 'DB_RECOVERY_FILE_DIST', defaultValue: 'default',description: 'destination for db_recovery')
			  booleanParam(name: 'refresh_configure', defaultValue: false, description: 'refresh only configuration')
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
					sh "ansible-galaxy install -f git+https://git.apps.okd.dcteam.local/oracle-ansible/install_oracle_home.git"
					sh "ansible-galaxy install -f git+http://git.apps.okd.dcteam.local/oracle-ansible/create_oracle_database.git"
					sh "ansible-galaxy install -f git+http://git.apps.okd.dcteam.local/oracle-ansible/install_patch.git"
				 }
			}
			stage('Install ORACLE_HOME')
			{
				steps{
						ansiblePlaybook([
											playbook: "install_oracle_home.yml",
											extraVars: [
											oracle_dbhome: env.ORACLE_HOME,
											db_name: env.ORACLE_DB_NAME,
											host_address: env.HOST_ADDRESS, 
											db_archive_mode: env.ARCHIVELOG_MODE,
											datafile_destination: env.DB_CREATE_FILE_DIST,
											recovery_destination: env.DB_RECOVERY_FILE_DIST
				   									   ]
		              					])
				}
			} 
		}
		}
	}
}
