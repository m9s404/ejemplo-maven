import groovy.json.JsonSlurperClassic

def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
pipeline {
    agent any

    
    stages {
        stage('SCM') {
            steps {
                git branch: 'sonar-feature', changelog: false, poll: false, url: 'https://github.com/m9s404/ejemplo-maven.git'
            }
        }
        stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv(credentialsId: 'SoniSecret', installationName: 'Sonita') {
            sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar \
                -Dsonar.target=sonar.java.binaries'
            }
            }
            
        }
        stage("Paso 1: Saludar"){
            steps {
                script {
                sh "echo 'Hello, World Usach!'"
                }
            }
        }
        stage("Paso 2: Crear Archivo"){
            steps {
                script {
                sh "echo 'Hello, World Usach!!' > hello-devops-usach-.txt"
                }
            }
        }
        stage("Paso 3: Guardar Archivo"){
            steps {
                script {
                sh "echo 'Persisitir Archivo!'"
                }
            }
            post {
                //record the test results and archive the jar file.
                success {
                    archiveArtifacts(artifacts:'**/*.txt', followSymlinks:false)
                }
            }
        }
    }
    post {
        always {
            sh "echo 'fase always executed post'"
        }
        success {
            sh "echo 'fase success'"
        }
        failure {
            sh "echo 'fase failure'"
        }
    }
}