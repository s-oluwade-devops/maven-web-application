pipeline
{
  agent any
  tools
  {
    maven 'maven 3.9.6'
  }
  stages
  {
    stage('1.Clone')
    {
      steps
      {
        sh "echo 'cloning the latest application version' "
        // git branch: 'dev_samuel', credentialsId: 'gitHubCredentials', url: 'https://github.com/SapphireSquadLandmarkOrg/maven-web-application.git'
        // git "https://github.com/SapphireSquadLandmarkOrg/maven-web-application.git"
        git branch: 'dev_samuel', url: 'https://github.com/SapphireSquadLandmarkOrg/maven-web-application.git'
      }
    }
    stage('2.Test+Build')
    {
      steps
      {
        sh "echo 'running JUnit-test-cases' "
        sh "echo 'testing must passed to create artifacts ' "
        sh 'mvn clean package'
      }
    }
    stage('3.CodeQuality')
    {
      steps
      {
        sh "echo 'Perfoming CodeQualityAnalysis' "
      // sh 'mvn sonar:sonar'
      }
    }
    stage('4.UploadArtifacts')
    {
      steps
      {
        sh 'echo deploying artifacts'
      // sh 'mvn deploy'
      }
    }
    stage('5.Deployment')
    {
      steps
      {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://10.0.15.44:8080/')], contextPath: null, war: 'target/*war'
      }
    }
  }
  // post
  // {
  //   always
  //   {
  //     emailext body: '''
  //     Please check build status.

  //     Thanks
  //     Samuel''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'samueloluwade.devops@gmail.com'
  //   }
  //   success
  //   {
  //     emailext body: '''
  //     Successful build.

  //     Thanks
  //     Samuel''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'samueloluwade.devops@gmail.com'
  //   }
  //   failure
  //   {
  //     emailext body: '''
  //     Build failed. Please resolve issues.

  //     Thanks
  //     Samuel''', recipientProviders: [buildUser(), developers()], subject: 'failure', to: 'samueloluwade.devops@gmail.com'
  //   }
  // }
}
