pipeline {
    agent { label 'Built-In' }  // Run the pipeline from Built-In Node

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[url: 'https://github.com/salman123-sudo/AgentCalling.git']]
                    ])
                }
                echo "Code fetched successfully!"
            }
        }

        stage('Execute on QA-AGENT') {
            agent { label 'QA-AGENT' }  // Switch execution to QA-AGENT
            steps {
                script {
                    echo "Running commands on QA-AGENT..."
                    sh 'ls -l /jenk/salman'  // Lists files in the directory
                }
            }
        }
    }
}
