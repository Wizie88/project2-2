pipeline {
    agent any

    tools {
        maven 'maven'
    }
    environment {
        ANSIBLE_HOME = "/path/to/ansible"
        PLAYBOOK_PATH = "path/to/your/playbook.yml"
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from version control (e.g., Git)
                git 'https://github.com/Wizie88/project2-2.git'
            }
        }

        stage('Run Ansible to install maven') {
            steps {
                script {
                    def ansiblePlaybookPath = 'maven.yml'
                    def repositoryUrl = 'https://github.com/Wizie88/project2-2.git'
                    // execute ansible playbook
                    sh "ansible-playbook -i localhost, ${ansiblePlaybookPath}"
                    )
                }
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
                // Build your Java web application (e.g., using Maven or Gradle)
                sh 'mvn clean package' // Adjust this command based on your build tool
                sh 'ls -la target'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests for your application
                sh 'mvn test' // Adjust this command based on your testing framework
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
                // Copy the built WAR file to Tomcat's webapps directory
               script { // Copy the WAR file to Tomcat's webapps directory
                    ansiblePlaybook credentialsId: 'f4', disableHostKeyChecking: true, installation: 'project2-1', inventory: 'hosts2.ini', playbook: 'deploy2yml', vaultTmpPath: ''
                }
                
                 
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded. App deployed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}