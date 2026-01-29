pipeline {
  agent any

  stages {

    stage('Clone Backend') {
      steps {
        dir('backend') {
          git 'https://github.com/caresync-hms/hms-backend.git'
        }
      }
    }

    stage('Build Backend Image') {
      steps {
        dir('backend') {
          sh 'mvn clean package -DskipTests'
          sh 'docker build -t hms-backend .'
        }
      }
    }

    stage('Clone Frontend') {
      steps {
        dir('frontend') {
          git 'https://github.com/caresync-hms/hms-frontend.git'
        }
      }
    }

    stage('Build Frontend Image') {
      steps {
        dir('frontend') {
          sh 'docker build -t hms-frontend .'
        }
      }
    }

    stage('Deploy') {
      steps {
        dir('deploy') {
          git 'https://github.com/caresync-hms/hms-deploy.git'
          sh 'docker-compose down'
          sh 'docker-compose up -d'
        }
      }
    }
  }
}
