
pipeline {
    agent { label 'ltecom'}
    stages {
        stage ('Clone') {
            steps {
                git branch: 'developer', url: "https://github.com/komali306/branchesofgol.git"
            }
        }

        stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "ARTIFACTORY",
                    url: "http://40.91.111.187:8082/artifactory",
                    credentialsId: "ARTIFACTORY01"
                )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "ARTIFACTORY",
                    releaseRepo: "libs-release-local",
                    snapshotRepo: "libs-snapshot-local"
                )

                rtMavenResolver (
                    id: "MAVEN_RESOLVER",
                    serverId: "ARTIFACTORY",
                    releaseRepo: "libs-release",
                    snapshotRepo: "libs-snapshot"
                )
            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MVN', // Tool name from Jenkins configuration
                    pom: '/jenkins/workspace/gol-qt_developer/pom.xml',
                    goals: 'mvn clean install',
                    deployerId: "MAVEN_DEPLOYER",
                    resolverId: "MAVEN_RESOLVER"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "ARTIFACTORY"
                )
            }
        }
    }
}


