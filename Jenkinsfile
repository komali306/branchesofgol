pipeline {
    agent { label 'MASTER'}
    stages {
        stage('scm') {
            steps {
                git branch: 'developer', url:'https://github.com/komali306/branchesofgol.git'        
            }
        }
        stage('build') {
            steps {
                sh script: 'mvn package'
            }
        }
        stage('post build') {
            steps {
                junit 'gameoflife-web/target/surefire-reports/*.xml'
                archiveArtifacts 'gameoflife-web/target/*.war'
            }
        }
    }
}


