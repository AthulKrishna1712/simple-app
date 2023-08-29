pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: '/var/lib/jenkins/workspace/nexus-pipeline/target/simple-app-3.0.0-SNAPSHOT.war', 
                        type: 'war'
                    ]
                ], 
                    credentialsId: 'nexus-repo', 
                    groupId: 'in.javahome', 
                    nexusUrl: '165.232.188.178:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'simple-app-release', 
                    version: '3.0.0-SNAPSHOT'
              
            }
        }
    }
}
