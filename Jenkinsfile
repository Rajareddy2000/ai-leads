pipeline {
  agent any
  stages {
    stage('checkout') {
      when {
        expression {
          return env.BRANCH_NAME == 'feature'
        }
      }
      steps {
        git branch: 'feature', url: 'https://github.com/Rajareddy2000/ai-leads'
      }
    }

    stage('maven build') {
      when {
        expression {
          return env.BRANCH_NAME == 'routelink'
        }
      }
      steps {
        sh 'mvn clean package'
      }
    }

    stage('tomcat deployment') {
      when {
        expression {
          return env.BRANCH_NAME == 'main'
        }
      }
      steps {
        sshagent(['tomcat-dev']) {
          // Copy war file to tomcat
          sh "scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.38.170:/opt/tomcat9/webapps"
          sh "ssh ec2-user@172.31.38.170 /opt/tomcat9/bin/shutdown.sh"
          sh "ssh ec2-user@172.31.38.170 /opt/tomcat9/bin/startup.sh"
        }
      }
    }
  }
}
