pipeline {
    agent any

    tools {
        jdk 'JDK17'
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
                ws("/var/jenkins_home/workspace/helloworld") {
                    sh 'mvn clean package -DskipTests=true -DfinalName=hello-world-demo'
                    archiveArtifacts artifacts: 'target/hello-world-demo.jar', fingerprint: true
                }
            }
        }
        stage("Unit Test") {
            steps {
                ws("/var/jenkins_home/workspace/helloworld") {
                    sh 'mvn test -Dsurefire.reportNameSuffix=-helloworld'
                    junit 'target/surefire-reports/TEST-*-helloworld.xml'
                }
            }
        }
        stage("Cleanup") {
            steps {
                ws("/var/jenkins_home/workspace/helloworld") {
                    sh 'mvn clean'
                }
            }
        }
    }
}
