pipeline {
    
    agent {
        label 'ecs'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'            
                // Build the Android App
                dir('testing_codelab/step_07/') {
                    sh 'flutter build appbundle'
                    
                    // Archive the Build Artifact on the created S3 Bucket
                    archiveArtifacts "/build/app/outputs/bundle/release/*"
                }
            }
        }
        stage('Check the Code Quality') {
            steps {
                dir('testing_codelab/step_07/') {
                    // Check the Code Quality
                    // Flutter Analyze performs a static analysis
                    // See here for more details: https://flutter.dev/docs/reference/flutter-cli#flutter-commands
                    echo 'Doing Code Quality Tests'
                    sh 'flutter analyze'
                }
            }
        }

        stage('Unit Tests') {
            steps {
                dir('testing_codelab/step_07/') {
                    // Run all unit tests
                    echo 'Doing Unit Tests'
                    sh 'flutter test test/models/favorites_test.dart'
                }
            }
        }
        
        stage('Widget Tests') {
            
            steps {
                dir('testing_codelab/step_07/') {
                    // Run all Widget tests on the code
                    echo 'Doing Unit Tests'
                    sh 'flutter run test/home_test.dart'
                }
            }
        }
        stage('Integration Tests') {
            steps {
                dir('testing_codelab/step_07/') {
                    // Running integration tests on AWS Devicefarm, uses Sylph and a config file
                    echo 'Running integrations tests on AWS Devicefarm...'
                    sh 'sylph -c sylph.yaml'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }

    }
    
    post {
        // Post Tasks
        always {
            echo "None so far..."
        }
    }
}
