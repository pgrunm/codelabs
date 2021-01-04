pipeline {
    
    agent {
        label 'ecs'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'            
                // Start with building the app
                //sh 'flutter create --no-overwrite testing_codelab/step_07/'
                sh 'pwd'
                dir('testing_codelab/step_07/') {
                    sh 'pwd'
                    sh 'flutter build appbundle'
                    
                    // Todo: Archive the Build Artifact.
                }
            }
        }
        stage('Check the Code Quality') {
            steps {
                dir('testing_codelab/step_07/') {
                    echo 'Doing Code Quality Tests'
                    sh 'flutter analyze'
                }
            }
        }

        stage('Unit Tests') {
            steps {
                dir('testing_codelab/step_07/') {
                    echo 'Doing Unit Tests'
                    sh 'flutter test test/models/favorites_test.dart'
                }
            }
        }
        
        stage('Widget Tests') {
            
            steps {
                dir('testing_codelab/step_07/') {
                    echo 'Doing Unit Tests'
                    sh 'flutter run test/home_test.dart'
                }
            }
        }
        stage('Integration Tests') {
            steps {
                echo 'TBD'
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
            echo "TBD"
        }
    }
}
