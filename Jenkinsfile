pipeline {
  agent {
    docker {
      image 'node:8.11.4'
      args '-u 0:0'
    }
  }

  stages {

    stage('Generate Config Files') {
      steps {
        script {
          checkout scm
          ENV_FILE = (BRANCH_NAME == 'master') ? 'config-production' : 'config-development'
        }
      }
    }

    stage('Build') {
      steps {
        script {
          configFileProvider([configFile(fileId: ENV_FILE, variable: 'FILE')]) {
            sh 'cat $FILE >> config.json'
            sh 'cat config.json'
            sh 'echo "HELLO WORLD"'
          }
        }
      }
    }

    stage('Test') {
      steps {
        script {
          sh 'echo "HELLO WORLD!!!"'
        }
      }
    }
    // stage ('Prepare') {
    //   steps {
    //     sh 'node --version; npm --version'
    //     sh 'npm install'
    //     sh 'ls -la ./node_modules'
    //     sh './node_modules/.bin/bower install --allow-root'
    //   }
    // }

    // stage ('Test') {
    //   steps {
    //     script {
    //       sh './node_modules/.bin/eslint --ext .js src/'
    //     }
    //   }
    // }
    // stage('Testing') {
      
    // }

    // stage('Build') {
    //   steps {
    //     script {
    //       sh 'tar -zcvf app.tar.gz src'
    //       sshagent(credentials: ['12d7fb99-10af-4997-9ab9-852768d34e79']) {
    //         sh 'scp -v -o StrictHostKeyChecking=no ./app.tar.gz root@104.248.51.10:/root'
    //         sh 'ssh -o StrictHostKeyChecking=no root@104.248.51.10 "sh build.sh"'
    //       }
    //     }
    //   }
    // }
  }
}
