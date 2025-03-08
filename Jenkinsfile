pipeline {
    agent any


    options {
        customWorkspace "/var/jenkins_home/workspace/helloworld"
    }

    tools {
        jdk 'JDK17' // Ensure Java 17 is used
        maven 'M399'
    }

    stages {
        stage("Check Java and Maven Version") {
            steps {
                sh 'echo "System Java Version:" && java -version'
                sh 'echo "Maven Java Version:" && mvn -v'
            }
        }
        stage("Build") {
            steps {
              //  git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Navarup/jenkins-hello-world'
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage("Unit Test"){
            steps{
                sh 'mvn test'
            }
        }
    }
}
