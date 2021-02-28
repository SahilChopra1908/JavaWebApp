node{
  stage('SCM Checkout'){
    git 'https://github.com/SahilChopra1908/JavaWebApp.git'
  }
  stage('Installing-Package'){
    bat 'C:\\Users\\SC185401\\Downloads\\apache-maven-3.6.3-bin\\apache-maven-3.6.3\\bin\\mvn -f FirstWebApp/pom.xml clean install'
  }
  stage('Compile-Package'){
    bat 'C:\\Users\\SC185401\\Downloads\\apache-maven-3.6.3-bin\\apache-maven-3.6.3\\bin\\mvn -f FirstWebApp/pom.xml package'
  }
  stage('SonarQube Analysis'){
    withSonarQubeEnv('sonar-6'){
      bat "C:\\Users\\SC185401\\Downloads\\apache-maven-3.6.3-bin\\apache-maven-3.6.3\\bin\\mvn sonar:sonar"
    }
  }
  stage("Quality Gate Analysis"){
    sleep 20
     timeout(time: 1, unit: 'HOURS') {
            def qg = waitForQualityGate()
            if (qg.status != 'OK') {
                  emailext body: '''Hi,
                  Please check the reason why the job got failed.
                  Regards,
                  Sahil''', subject: 'Jenkins Job Status', to: 'sahil.chopra0897@gmail.com'
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
  }
  stage('Email notification'){
    emailext body: '''Hi,
                  Job Success.
                  Regards,
                  Sahil''', subject: 'Jenkins Job Status', to: 'sahil.chopra0897@gmail.com'
      }
}
