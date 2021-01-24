pipeline {
    
    agent {
        // Tells the pipeline to use an AWS ECS agent,
        // because of the used label.
        label 'ecs'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'            
                // Build the Android App
                dir('testing_codelab/step_07/') {
                    sh 'flutter build appbundle'
                    
                    // Archive the Build Artifact on the 
                    // created S3 Bucket.
                    archiveArtifacts "/build/app/outputs/bundle/release/*"
                }
            }
        }
        stage('Check the Code Quality') {
            steps {
                dir('testing_codelab/step_07/') {
                    // Check the Code Quality
                    // Flutter Analyze performs a static analysis
                    // See here for more details: 
                    // https://flutter.dev/docs/reference/flutter-cli#flutter-commands
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
                    // Point to Unit Test directory
                    // Coverage is reported to ./coverage/lcov.info
                    sh 'flutter test --coverage test/models/'
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

        stage('Beta Deployment') {
            // Deploy as Beta Release if no there is no git tag
            when { 
                not { 
                    buildingTag() 
                } 
            }

            steps {
                echo 'Deploying beta version to Play Store'
                sh 'fastlane beta'
            }
        }
        stage('Release Deployment') {
            // Deploy as full release if the current commit contains a git tag
            // Captures screenshots and uploads the app file to playstore
            when { 
                buildingTag() 
            }
            steps {
                echo 'Deploying release version to Play Store'
                sh 'fastlane playstore'
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
