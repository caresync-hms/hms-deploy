pipeline {
  agent any

  stages {

    stage('Clone Backend') {
      steps {
        dir('backend') {
          git branch: 'main',
              url: 'https://github.com/caresync-hms/hms-backend.git',
              credentialsId: 'github-token'
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
          git branch: 'main',
              url: 'https://github.com/caresync-hms/hms-frontend.git',
              credentialsId: 'github-token'
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
        sh 'docker-compose down'
        sh 'docker-compose up -d'
      }
    }
  }
}
