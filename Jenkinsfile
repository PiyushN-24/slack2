pipeline {
    agent any
    
    triggers {
        pollSCM '* * * * *'
    }
    
    parameters {
        choice choices: ['DEV', 'QA', 'UAT'], name: 'Environment'
    }

    stages {
        stage('CheckOut') {
            steps {
                checkout scm
            }
        }
        stage('Validate') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn validate'
            }
        }
	stage('Compile') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn compile'
            }
        }
	stage('Test') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn test'
            }
        }
	stage('Package') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn package'
            }
        }
	stage('Verify') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn verify'
            }
        }
	stage('Install') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn install'
            }
        }
        stage('Deployment') {
            steps {
                sh 'cp target/slack2.war /home/therecker/DevOps/Maven/apache-tomcat-9.0.85/webapps/'
            }
        }
	stage('Slack Notification') {
	    steps {
		slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#slack-notification2', color: 'good', message: 'Welcome to Slack via Jenkins', teamDomain: 'DevOps', tokenCredentialId: 'slack-notification2', username: 'therecker2418'
	    }
	}
    }
}
