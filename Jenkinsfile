pipeline
{
agent any
  
  tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven_3_5_2"
    }
  stages{
    stage('Build1'){
      steps{
        checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ganate34/webgoat.git/']])
      }
    }
    stage('Build2') {
      steps {
           // Get some code from a GitHub repository
           git 'https://github.com/ganate34/webgoat.git/'

          // Run Maven on a Unix agent.
          sh "mvn -Dmaven.test.failure.ignore=true clean package"

          // To run Maven on a Windows agent, use
          // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
    stage('Pre-Test'){
        steps{
          sleep time: 5, unit: 'MILLISECONDS'
        }
      }
    stage('Test1'){
      steps{
        sh 'java --version'
      }
    }
    stage('Test2'){
      steps{
        sh 'mvn --version'
      }
    }
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dmaven.test.skip=true -Dmaven.test.failure.ignore=true  -Dsonar.projectKey=ganate34github-test1 -Dsonar.organization=ganate34github -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=953115046d6108cbd76287ea98a735f6cd7c7df8'
			}
    }
  }
}
