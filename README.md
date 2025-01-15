# SE_practice

pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME' // Ensure Maven is configured correctly in Jenkins
    }
    stages {
        stage('Git Clone and Clean') {
            steps {
                script {
                    try {
                        // Use absolute paths to avoid dependency on configurations
                        bat 'C:\\Windows\\System32\\cmd.exe /c rmdir /s /q maven'
                        bat 'C:\\Windows\\System32\\cmd.exe /c git clone https://github.com/lxksh/maven.git'
                    } catch (Exception e) {
                        echo "Git clone or clean failed: ${e}"
                    }
                }
            }
        }
        stage('Maven Clean') {
            steps {
                script {
                    try {
                        bat '"C:\\Program Files\\apache-maven-3.9.9\\bin\\mvn.cmd" clean -f maven'
                    } catch (Exception e) {
                        echo "Maven clean failed: ${e}"
                    }
                }
            }
        }
        stage('Maven Install') {
            steps {
                script {
                    try {
                        bat '"C:\\Program Files\\apache-maven-3.9.9\\bin\\mvn.cmd" install -f maven'
                    } catch (Exception e) {
                        echo "Maven install failed: ${e}"
                    }
                }
            }
        }
        stage('Maven Test') {
            steps {
                script {
                    try {
                        bat '"C:\\Program Files\\apache-maven-3.9.9\\bin\\mvn.cmd" test -f maven'
                    } catch (Exception e) {
                        echo "Maven test failed: ${e}"
                    }
                }
            }
        }
        stage('Maven Package') {
            steps {
                script {
                    try {
                        bat '"C:\\Program Files\\apache-maven-3.9.9\\bin\\mvn.cmd" package -f maven'
                    } catch (Exception e) {
                        echo "Maven package failed: ${e}"
                    }
                }
            }
        }
    }
}
