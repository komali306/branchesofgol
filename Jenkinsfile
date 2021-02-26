pipeline {
    agent { label 'ltecom'}
    triggers {
        cron('59 23 * * ')
    }
    stages {
        stage('scm') {
            steps {
                git branch :'qa', url: 'https://github.com/komali306/branchesofgol.git'        
            }
        }
        stage('build') {
            steps {
                sh script: 'mvn clean package'
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