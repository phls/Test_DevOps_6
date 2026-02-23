pipeline {
    agent none

    stages {
        stage('Lint') {
            agent { label 'agent1' } 
            steps {
                sh '''
                cd calculator
                make clean
                make check
                '''
            }
        }
        stage('Build') {
            agent { label 'agent1' } 
            steps {
                sh '''
                cd calculator
                make
                '''
                archiveArtifacts artifacts: 'calculator/bin/*', fingerprint: true 
            }
        }
        stage('Test') {
            agent { label 'agent2' } 
            steps {
                sh '''
                cd calculator
                make unittest
                '''
                archiveArtifacts artifacts: 'calculator/tests/bin/*', fingerprint: true 
            }
        }  
    }
}