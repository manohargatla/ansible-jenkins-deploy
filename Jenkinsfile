pipeline {
    agent { label 'jenkins_node' }
    stages {
        stage('clone sources') {
            steps {
                git branch: 'main',
                url: 'https://github.com/manohargatla/ansible-jenkins-deploy.git' 
            }
        }
        stage('clone repo') {
            steps {
               
                sh """
                if [ -d "spring-petclinic" ] 
                then
                    echo "Directory spring-petclinic exists." 
                    cd spring-petclinic
                    git pull
                    ./mvnw package
                    cd ..
                    pwd
                else
                    git clone https://github.com/manohargatla/spring-petclinic.git
                    cd spring-petclinic
                    ./mvnw package
                    cd ..
                    pwd
                fi
                
                """
            }
        }
        // stage('build package') {
        //     steps {
        //         sh 'cd ${WORKSPACE} && ./mvnw package'
        //     }
        // }
        stage('apply playbook') {
            steps {
                sh 'ansible -i ~/hosts -m ping all'
                sh 'ansible-playbook -i ~/hosts spring-petclinic.yaml'
            }
        }
        
    }
}