pipeline {
  agent any

  environment {
    PYTHON = 'C:\\Users\\j\\AppData\\Local\\Programs\\Python\\Python311\\python.exe'
  }

  stages {
    stage('Hello') {
      steps {
        echo 'Hello depuis un pipeline declaratif'
      }
    }
    stage('Infos environnement') {
      steps {
        echo "Nom du noeud Jenkins: ${env.NODE_NAME}"
        echo "Workspace: ${env.WORKSPACE}"
      }
    }
    stage('Installation') {
      steps {
        bat "${env.PYTHON} --version"
        bat "${env.PYTHON} -m venv venv"
        bat 'venv\\Scripts\\python -m pip install --upgrade pip'
        bat 'venv\\Scripts\\python -m pip install -r requirements.txt'
      }
    }
    stage('Tests') {
      steps {
        bat 'venv\\Scripts\\python -m pytest -v --junitxml=reports\\results.xml'
      }
    }
  }

  post {
    always {
      junit allowEmptyResults: true, testResults: 'reports/results.xml'
    }
    success {
      echo 'Pipeline termine avec succes'
    }
    failure {
      echo 'Le pipeline a echoue'
    }
  }
}
