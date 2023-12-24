pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Check if 'build' directory exists
                    def buildDir = 'build'
                    def buildDirExists = fileExists(buildDir)

                    // Create 'build' directory if it doesn't exist
                    if (!buildDirExists) {
                        bat "mkdir ${buildDir}"
                    }

                    // Create 'car.txt' file with content
                    bat "echo tesla cybertruck > ${buildDir}\\car.txt"

                    // Append "engine" and "horsepower" to 'car.txt'
                    bat "echo engine >> ${buildDir}\\car.txt"
                    bat "echo horsepower >> ${buildDir}\\car.txt"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    def buildDir = 'build'
                    def fileContent = readFile("${buildDir}\\car.txt").trim()

                    if (fileContent.contains('tesla cybertruck') && fileContent.contains('engine') && fileContent.contains('horsepower')) {
                        echo 'Content check passed: "tesla cybertruck", "engine", and "horsepower" found in car.txt'
                    } else {
                        error 'Content check failed: Unexpected content in car.txt'
                    }
                }
            }
        }

        stage('Publish') {
            steps {
                archiveArtifacts 'build/**/*'
            }
        }
    }
}
