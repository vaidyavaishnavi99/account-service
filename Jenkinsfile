node{
 def MAVEN_HOME = tool "mymaven"
 env.PATH = "${env.PATH}:${MAVEN_HOME}/bin"
  
  stage('checkout'){  
       checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/raj11222021/account-service.git']]])
  }
  stage('compile'){
      sh 'mvn clean compile'
  }
  
  
  stage('unit testing'){
      sh 'mvn test'
        
    }
      stage('Code quality analysis') 
	{
		withSonarQubeEnv('Newsonar') 
		{
                 sh 'mvn sonar:sonar -Dsonar.organization=vaidyavaishnavi99 -Dsonar.projectKey=Firstsonar'

		
    		}
}
  
  stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }
}
  
  
    
		
    		
