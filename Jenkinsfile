pipeline {
    agent { label 'ansible_jenkins' }
    stages {
        stage('clone sources') {
            steps {
                git branch: 'main'
                url: 'https://github.com/manohargatla/ansible-jenkins-deploy.git' 
            }
        }
        stage('clone sources') {
            steps {
                sh 'git clone https://github.com/manohargatla/spring-petclinic.git' 
            }
        }
        stage('build package') {
            steps {
                sh 'cd ${WORKSPACE} && ./mvnw package'
            }
        }
        stage('apply playbook') {
            steps {
                sh 'ansible -i hosts -m ping all'
                sh 'ansible-playbook -i hosts spring-petclinic.yaml'
            }
        }
        
    }
}