pipeline {
    agent {
     kubernetes {
       yamlFile 'AgentPod.yaml'
         }
    }
    environment{
        AI_RESEARCH_SAAMA = '381743254372'
        LSACONE_DEV = '791532114280'
    }
    stages {
        stage('Assume Role in Dev') {
            steps {
                container('swashikan'){
                script {
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: 'app.jenkins.ecr-migration',
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                    ]]) {
                        withAWS(roleAccount: '381743254372', role: 'arn:aws:iam::381743254372:role/app.jenkins.ecr-migration.role') {
                            // Your AWS CLI commands or AWS SDK operations here
                            sh 'aws s3 ls'  // Example command, replace with your actual AWS commands
                        }
                    }
                }
              }
            }
        }
    }
}