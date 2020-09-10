pipeline {
    agent any
	stages{

    stage('Start preparing with ansible-galaxy') {
	steps {
	  sh "ansible-galaxy install git+https://git.apps.okd.dcteam.local/oracle-ansible/install_oracle_home.git"
       ansiblePlaybook([
		playbook: "test.yml",
		inventory: "inventory"
		               ])
		}
    }
		}
}
