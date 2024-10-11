pipeline{
    agent any
    
    stages{
        stage("Git Checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/Rajareddy2000/ai-leads'
            }
        }
        stage("Maven Build"){
             steps {
                echo 'Building Maven Project'
                // Add your Maven build commands here, for example:
                // sh 'mvn clean install'
            }
           
        }
        stage("Tomcat Deploy - Dev"){
            steps{
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
