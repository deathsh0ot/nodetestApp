node {
     environment {
            CI = 'true'
        }
        stage('checkout') {
            
                 echo 'Copying...'
                git 'https://github.com/deathsh0ot/nodetestApp.git'
            
        }
        stage('Build') {
            
                sh 'npm install'
            
        }
        stage('Test') {
                
                        sh './jenkins/scripts/test.sh'
                    
                }
        stage('SonarQube analysis') {
             
            def scannerHome = tool 'sonar_scanner';
            withSonarQubeEnv('SonarQ') {
            sh "${scannerHome}/bin/sonar-scanner  -Dsonar.projectKey=develop"
            
    }
  }
  stage("building image") {
        sh 'docker build -t nodeappj ${WORKSPACE}/src/Dockerfile'
      }
  stage("run") {
        sh ' docker run --rm -p 3000:3000 nodeappj'
        
      }
    
}