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

        stage('Commit and push artifact') {
            steps {
                script {
                     def gitUsername = 'K-Sowjanya'
                    def artifactPath = "target/*.jar"
                    
                    env.GIT_AUTHOR_NAME = gitUsername
                    env.GIT_COMMITTER_NAME = gitUsername
                    
                    sh "git config --global user.name '${gitUsername}'"
                    
                    sh "git add ${artifactPath}"
                    sh "git commit -m 'Add built artifact'"
                    sh "git push ${env.gittoken} HEAD:refs/heads/main"
                }
            }
        }
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
