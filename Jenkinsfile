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
                checkout scm
            }
        }

        stage('Run Ansible') {
            steps {
                script {
                // Ensure the Ansible binary is in the PATH
                ansibleHome = tool 'ansible'
                ansiblePlaybook = "${ansibleHome}/bin/ansible-playbook"
                // Execute the Ansible playbook
                sh "${ansiblePlaybook} -i inventory_file ${PLAYBOOK_PATH}"
                }
            }
        }       

        stage('Build') {
            steps {
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
                    sh "cp ${WAR_FILE_PATH} ${TOMCAT_WEBAPPS_DIR}/${APP_NAME}.war"
                }
                
                 
            }
        }
    }
}