pipeline { 
  agent any
  tools {nodejs "node"}
  
  stages { 
    stage('clone the repo') {
      steps { 
        git 'https://github.com/digitaltangent/gallery-new.git'
        slackSend(channel: "#aleedaip1", message: "git clone success!")
      }
    }
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Start MongoDB') {
      steps {
        sh 'mongod'
      }
    }
    stage('Tests') {
      steps { 
        sh 'npm test'
      }
    }
stage('Deploy to Heroku') {
  steps {
    withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS' )]){
      sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/immense-thicket-43199.git master'
      slackSend(channel: "#aleedaip1", message: "Testing Slack from Jenkins!")
    }
  }
}
//stage('Start node') {
  //steps {
   //sh 'node server'
  //}
//}      
    
  
  }
}