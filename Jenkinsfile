pipeline
{
    agent any
    stages
    {
        stage(ContinuousDownload)
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage(ContinuousBuild)
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage(ContinuousDeployment)
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '22bc17ec-3ba2-49c2-9344-6892f7e2d51f', path: '', url: 'http://172.31.24.215:8080')], contextPath: 'sa', war: '**/*.war'
            }
        }
         stage(ContinuousTesting)
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/Declarative_pipeline2/testing.jar'
                
            }
        }
        stage(ContinuousDelivery)
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '22bc17ec-3ba2-49c2-9344-6892f7e2d51f', path: '', url: 'http://172.31.26.76:8080')], contextPath: 'pa', war: '**/*.war'
            }
        }
    }
}
