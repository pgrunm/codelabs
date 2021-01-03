pipeline {
    
    agent {
        label 'ecs'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'cd testing_codelab/step_07/'
                
                // Start with building the app
                sh 'flutter create --no-overwrite .'
                sh 'flutter build appbundle'
            }
        }
        stage('Check the Code Quality') {
            steps {
                echo 'Doing Code Quality Tests'
                sh 'flutter analyze'
            }
        }

        stage('Unit Tests') {
            steps {
                echo 'Doing Unit Tests'
                sh 'flutter test test/models/favorites_test.dart'
            }
        }
        
        stage('Widget Tests') {
            steps {
                echo 'Doing Widget Tests'
                sh 'flutter run test/home_test.dart '
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
    }
}