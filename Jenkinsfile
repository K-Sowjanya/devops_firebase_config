pipeline {
    agent any

 

    environment {
        mavenTool = 'Maven 3.9.4'
    }

    stages {
        stage('Checkout code') {
            steps {
                checkout scm
            }
        }

 

        stage('Set up JDK') {
            steps {
                tool name: 'JDK 17', type: 'jdk'
            }
        }

 

        stage('Build with Maven') {
            steps {
                tool name: mavenTool, type: 'hudson.tasks.Maven$MavenInstallation'
                bat "\"${tool(name: mavenTool, type: 'hudson.tasks.Maven$MavenInstallation')}/bin/mvn\" -B clean compile package --file token/pom.xml"
            }
        }

       stage('Store artifact') {
            steps {
                bat 'copy "token\\target\\*.jar" "artifacts\\"'
            }
        }

        // stage('Commit and push artifact') {
        //     steps {
        //         script {
        //             checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'f7c6abff-a599-4765-937d-0c9e7009bebd', url: 'https://github.com/K-Sowjanya/devops_firebase_config.git']]])
        //             bat 'git add artifacts/'
        //             bat 'git commit -m "Add built artifact"'
        //             bat 'git push origin HEAD:refs/heads/main'
        //         }
        //     }
        // }
        stage('Compile and Run Java Program') {
            steps {
                script{
                def javaCmd = "${tool(name: 'JDK 17', type: 'jdk')}/bin/java"
                bat "\"${javaCmd}\" Firebase-0.0.1-SNAPSHOT.jar java.com.google.firebase.samples.config.TemplateConfigure"
                }
            }
        }
    }
}
