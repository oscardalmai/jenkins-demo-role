pipeline {
  agent any
  stages {
    stage ('Molecule test') {
      agent {
        docker {
          image 'quay.io/ansible/molecule:3.0.2'
          args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
         }
      }
      steps {
        sh 'molecule test'
      }
    }
    
    stage('Ansible Tower - Workflow execution') {
      steps {
        ansibleTower(towerServer: 'AWX TEST', towerCredentialsId: '5372add5-75b6-4f30-8dbc-8e5dc7eebdac', jobTemplate: '43', jobType: 'run', templateType: 'workflow', importWorkflowChildLogs: true, importTowerLogs: true, scmBranch: "${env.BRANCH_NAME}")
      }
    }
  }
}
