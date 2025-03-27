pipeline {
    agent { label 'Built-In Node' }  // Run from Built-In Node

    options {
        timestamps()  // Enable timestamps in logs
    }

    stages {
        stage('Start') {
            steps {
                echo "🚀 Starting the pipeline..."
            }
        }

        stage('Checkout Code') {
            steps {
                script {
                    echo "📥 Fetching code from GitHub..."
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/salman123-sudo/AgentCalling.git'
                        ]]
                    ])
                }
                echo "✅ Code fetched successfully!"
            }
        }

        stage('Execute on QA-AGENT') {
            agent { label 'QA-AGENT NODE' }  // Run this stage on QA-AGENT
            steps {
                script {
                    echo "🔍 Running commands on QA-AGENT NODE..."
                    sh '''
                        echo "📌 Listing Files in /opt/agent-slave"
                        ls -l /opt/agent-slave || echo "⚠️ Directory not found!"
                    '''
                }
            }
        }

        stage('End') {
            steps {
                echo "🎯 Pipeline execution completed successfully!"
            }
        }
    }

    post {
        always {
            echo "🛑 Pipeline Finished!"
        }
    }
}
