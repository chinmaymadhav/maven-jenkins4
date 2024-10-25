pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'java17'
    }
    stages {
        stage('Download-Git') {
            steps {
                echo "Downloading code from GIT"
                git branch: 'main', url: 'https://github.com/chinmaymadhav/maven-jenkins4.git'
            }
        }
        stage('Build') {
            steps {
                echo "Build using Maven"
                sh 'mvn clean package'
            }
        }
        stage('Archive-artifact') {
            steps {
                echo "Archive the artifacts"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
         stage('Trigger Deploy Job'){
            steps{
                echo "Building from other project"
                build wait: false, job: 'pipepine-deploy'
            }
        }
    }
}
