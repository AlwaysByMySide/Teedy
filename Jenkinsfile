pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean install' 
            }
        }
        stage('test') {
            steps {
                sh 'mvn test --fail-never '
            }
        }
        stage('Doc') { 
            steps {
                sh 'mvn javadoc:javadoc --fail-never' 
            }
        }
        stage('Pmd') { 
            steps {
                sh 'mvn pmd:pmd' 
            }
        }
        stage('TestReport') { 
            steps {
                sh 'mvn surefire-report:report'
                sh 'mvn jacoco:report' 
            }
        }
        
        
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
