pipeline
{
    agent any
    stages
    {
        stage('continuous download')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage('continuous Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '3a68ba8e-8531-4217-a2fa-c56ad3dffe16', path: '', url: 'http://172.31.32.51:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('continuous testing')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '3a68ba8e-8531-4217-a2fa-c56ad3dffe16', path: '', url: 'http://172.31.32.24:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
