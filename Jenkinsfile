pipeline {
    agent any

    stages {
        stage('Preparation') {
            steps {
                script {
                    // Clean up the workspace directory if it exists
                    if (fileExists('canaraswayam***')) {
                        sh 'rm -rf canaraswayam***'
                    }
                }
            }
        }

        stage('Checkout Code') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'AzureCredential', variable: 'AzureCredential')]) {
                        // Clone the Azure DevOps repository using the PAT without exposing it in the command
                        sh 'git clone https://${AzureCredential}@ID'
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Navigate to the 'canaraswayam' directory
                    dir('canaraswayam***') {
                        // Run npm install -force
                        sh 'npm install -force'

                        // Navigate to the 'android' directory
                        dir('android') {
                            // Grant execute permission to the gradlew script
                            sh 'chmod +x gradlew'

                            // Run the Gradle build command to generate the APK
                            sh './gradlew assembleDebug'  // Use 'assembleRelease' for a release APK
                        }
                    }
                }
            }
        }

        // Add more stages or post-build actions as needed
    }
}
