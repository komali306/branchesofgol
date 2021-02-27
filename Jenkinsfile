pipeline {
    agent { label 'ltecom'}
    stages {
        stage('scm') {
            steps {
                git branch: 'release', url:'https://github.com/KhajasCICDSamples/qt-gol.git'        
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
    post {
        always {
            (mail to 'pasupuletikomali6043@gmail.com'),
                subject : "status of pipeline ${currentBuild.fullDisplayName}",
                body: "${env.BUILD_URL}" has result ${currentBuild.result}
        }
    }
}


