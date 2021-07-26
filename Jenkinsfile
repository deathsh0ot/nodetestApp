node {
     environment {
            CI = 'true'
        }
        stage('checkout') {
            
                 echo 'copying...'
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
        sh 'docker build -f -t nodeappj /var/lib/jenkins/workspace/nodeApp/'
      }
  stage("run") {
        sh ' docker run --rm -p 3000:3000 nodeappj'
        
      }
    
}