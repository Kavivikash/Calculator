// This is a declarative Jenkins Pipeline script.
pipeline {
    // 'agent any' means this pipeline can run on any available agent (node).
    agent any

    // 'stages' contains the sequence of operations for the pipeline.
    stages {
        // Stage 1: Checkout code from the Git repository.
        stage('Checkout Code') {
            steps {
                // The 'git' step clones the repository.
                // Replace '<repository_url>' with your Git repo URL.
                // Replace '<branch_name>' with the branch you want to build.
                // 'credentialsId' should be the ID of your stored credentials in Jenkins.
                git branch: '<branch_name>', credentialsId: '<your_credentials_id>', url: '<repository_url>'
            }
        }

        // Stage 2: Build the project.
        stage('Build Project') {
            steps {
                // This script assumes your build script is at the root of the project.
                // If it's in a subdirectory, add a 'dir' block.
                // Example: dir('<path_to_your_project>') { sh './build.sh' }
                sh './build.sh'
            }
        }

        // Stage 3: Run tests.
        stage('Run Tests') {
            steps {
                // This script assumes your test script is at the root of the project.
                sh './test.sh'
            }
        }
    }

    // 'post' defines actions that run at the end of the pipeline run.
    post {
        // 'always' will run regardless of the pipeline's success or failure.
        always {
            echo 'Pipeline finished. Archiving logs...'
            // 'archiveArtifacts' saves files for later use.
            // This example archives all files ending in .log.
            archiveArtifacts artifacts: '**/*.log'
        }

        // 'success' runs only if the pipeline is successful.
        success {
            echo 'Pipeline was successful!'
            // You can add notification steps here, e.g., for Slack or email.
        }

        // 'failure' runs only if the pipeline fails.
        failure {
            echo 'Pipeline failed.'
            // You can add notification steps here to alert the team.
        }
    }
}
