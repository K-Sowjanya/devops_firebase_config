pipeline {
    agent any

    environment {
        mavenTool = 'Maven 3.9.4'
<<<<<<< HEAD
        gitRemoteUrl = 'https://github.com/shivanititan/Firebase-Remote.git'
=======
>>>>>>> 852d37ba3d083d439bf1cc8a02ef1c921db8f762
    }

    stages {
        stage('Checkout code') {
            steps {
                checkout scm
            }
        }

        stage('Set up JDK') {
            steps {
                tool name: 'JDK11', type: 'jdk'
            }
        }

        stage('Build with Maven') {
            steps {
                tool name: mavenTool, type: 'hudson.tasks.Maven$MavenInstallation'
<<<<<<< HEAD
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
                    def javaCmd = "${tool(name: 'JDK11', type: 'jdk')}/bin/java"
                    bat "\"${javaCmd}\" -cp \"C:/ProgramData/Jenkins/.jenkins/workspace/firebase-config/Firebase-Remote/target/Firebase-1.0-SNAPSHOT.jar\" com.example.Main"
                }
            }
        }
=======
                bat "\"${tool(name: mavenTool, type: 'hudson.tasks.Maven$MavenInstallation')}/bin/mvn\" -B clean compile package --file token/pom.xml"
            }
        }

        stage('Store artifact') {
            steps {
                bat 'copy "token\\target\\*.jar" "artifacts\\"'
            }
        }

        stage('Commit and push artifact') {
            environment {
                GIT_REPO_NAME = 'devops_firebase_config'
                GIT_USER_NAME = 'K-Sowjanya'
            }
            steps {
                script {
                    withCredentials([string(credentialsId: 'gittoken', variable: 'GITHUB_TOKEN')]) {
                        bat '''
                    git config user.email "konudulasowjanya13@titan.co.in"
                    git config user.name "K-Sowjanya"
                    git add artifacts/.
                    git commit -m "Update deployment image to version"
                    git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:main
                '''
                    }
                }
            }
        }

        stage('Compile and Run Java Program') {
            steps {
                script {
                    def javaCmd = "${tool(name: 'JDK 17', type: 'jdk')}/bin/java"
                    bat "\"${javaCmd}\" Firebase-0.0.1-SNAPSHOT.jar java.com.google.firebase.samples.config.TemplateConfigure"
                }
            }
        }
>>>>>>> 852d37ba3d083d439bf1cc8a02ef1c921db8f762
    }
}