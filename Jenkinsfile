pipeline { // For Job F/G
    agent any
    options { timestamps () }
    tools {
        maven 'M362auto'
    }
    //triggers { pollSCM '*/5 * * * *' }
    stages {
        stage('Preparation') {
            steps {
                cleanWs()
                git branch: "${env.BRANCH}", credentialsId: '18bc401b-7960-4d77-bd8d-6e75cfdf8a3d', url: 'git@github.com:maqsLV/spring-petclinic.git'
            }
        }
        stage('Build and test') {
            steps {
                sh 'mvn clean test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package -Dmaven.test.skip=true'
            }
        }
        stage('Deploy ^^') {
            when {
                branch 'master'
            }
            steps {
                rtUpload (
                serverId: 'ArtiForStudents',
                spec: '''{
                    "files": [
                        {
                        "pattern": "target/*.jar",
                        "target": "test/com/epam-labs/"
                        }
                    ]
                }'''
                )
            }
        }
    }
}