import groovy.json.JsonSlurperClassic

def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
pipeline {
    agent any

    
    stages {
        
        // stage('Sonarqube') {
        //     environment {
        //         scannerHome = tool 'SonarQubeScanner'
        //     }
        //     steps {
        //         withSonarQubeEnv('sonarqube') {
        //             sh "${scannerHome}/bin/sonar-scanner"
        //         }
        //         timeout(time: 10, unit: 'MINUTES') {
        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }
        stage('Sonarqube') {
            node {
            stage('SCM') {
                git 'https://github.com/m9s404/ejemplo-maven.git'
            }
            stage('SonarQube analysis') {
                withSonarQubeEnv(credentialsId: 'SoniSecret', installationName: 'Sonita') {
                sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
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