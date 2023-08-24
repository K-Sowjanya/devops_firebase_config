pipeline {
    agent any

    environment {
        mavenTool = 'Maven 3.9.4'
        gitRemoteUrl = 'https://github.com/shivanititan/Firebase-Remote.git'
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
               bat "\"${tool(name: mavenTool, type: 'hudson.tasks.Maven$MavenInstallation')}/bin/mvn\" -B clean compile package --file Firebase-Remote/pom.xml"
            }
        }

        // stage('Store artifact') {
        //     steps {
        //         script {
        //             def artifactDir = "D:\\artifacts" // Use forward slash (/) for paths in Jenkins
                
        //             if (!fileExists(artifactDir)) {
        //                 bat "mkdir \"${artifactDir}\""
        //             }

        //           bat "copy firebase-config\\Firebase-Remote\\target\\*.jar ${artifactDir}\\"
        //         }
        //     }
        // }

        stage('Compile and Run Java Program') {
            steps {
                script {
                    def javaCmd = "${tool(name: 'JDK 17', type: 'jdk')}/bin/java"
                    bat "\"${javaCmd}\" -cp \"C:/ProgramData/Jenkins/.jenkins/workspace/firebase-config/Firebase-Remote/target/Firebase-1.0-SNAPSHOT.jar\" com.example.Main"
                }
            }
        }
    }
}
