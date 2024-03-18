pipeline {
    agent any
    
    stages {
        stage ('Build') {
            steps {
                // Checkout code from Git repo
                git 'https://github.com/yankils/hello-world.git'
                
                // Build using Maven
                sh 'mvn clean package'
                
            }
        }
        
        stage ('Deploy to Docker') {
            steps {
                // Run Docker commands to deploy the WAR file to Tomcat in a Docker container
                sh '''
                    docker build -t tomcat .
                    docker tag tomcat harshaprasad21/tomcat
                    docker run -d -p 8070:8080 --name harshadocker harshaprasad21/tomcat
                    docker cp /var/lib/jenkins/workspace/pipeline/webapp/target/webapp.war harshadocker:/usr/local/tomcat/webapps
                    docker login -u harshaprasad21 -p Kungfupanda21*
                    docker push harshaprasad21/tomcat 
                '''
            }
        }
    }
}
