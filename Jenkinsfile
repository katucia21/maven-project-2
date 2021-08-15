pipeline {
  agent any
  environment {
    WORKSPACE = "${env.WORKSPACE}"
  }
  tools {
    maven 'localMaven'
    jdk 'localJdk'
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
      post {
        success {
          echo ' now Archiving '
          archiveArtifacts artifacts: '**/*.war'
        }
      }
    }
    stage('SonarQube Scan') {
      steps {
        sh """mvn sonar:sonar \
<<<<<<< HEAD
<<<<<<< HEAD
  -Dsonar.host.url=http://54.87.36.213:9000 \
=======
  -Dsonar.host.url=http://18.212.244.175:9000 \
>>>>>>> 5964fc2464bbc191e58ff731697bea310f3a90d2
=======
  -Dsonar.host.url=http://54.87.36.213:9000 \
>>>>>>> ea080036df1266827556a838a69001db823f8a56
  -Dsonar.login=8115a74f7c9bbc78ac7e348d711d362bfcd578a3
      }
    }
    stage('Upload to Artifactory') {
      steps {
        sh "mvn clean deploy -DskipTests"
      }

    }
    stage('Deploy to DEV') {
      environment {
        HOSTS = "dev"
      }
      steps {
        sh "ansible-playbook ${WORKSPACE}/deploy.yaml --extra-vars \"hosts=$HOSTS workspace_path=$WORKSPACE\""
      }

    }
    stage('Approval') {
      steps {
        input('Do you want to proceed?')
      }
    }
    stage('Deploy to PROD') {
      environment {
        HOSTS = "prod"
      }
      steps {
        sh "ansible-playbook ${WORKSPACE}/deploy.yaml --extra-vars \"hosts=$HOSTS workspace_path=$WORKSPACE\""
      }
    }
  }

}
