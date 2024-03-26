pipeline
{
    agent any
    stages
    {
        stage('ContinousDownload')
        {
            steps
            {
                git 'https://github.com/satish016/real-app.git'
            }
        }
        stage('ContinousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '9454aaf0-dccd-491c-a2c3-2ca60e0fdf79', path: '', url: 'http://172.31.11.230:8080')], contextPath: 'qadeclare', war: '**/*.war'
            }
        }
        stage('ContinousTestingt')
        {
            steps
            {
                git 'https://github.com/satish016/testing.git'
                sh 'java -jar /var/lib/jenkins/workspace/dev/testing.jar'
            }
        }
        stage('ContinousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'c06eb8fb-a30a-4d60-b148-d4fb5e6439d3', path: '', url: 'http://172.31.7.174:8080')], contextPath: 'proddeclare', war: '**/*.war'
            }
        }
        
    }
}