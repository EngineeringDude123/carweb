node('App-Server-CWEB2140')
{
    def app
    stage('Cloning Git')
    {
        checkout scm
    }

    stage('Build and Tag')
    {
        app = docker.build('johncollegeacc769/carweb')
    }

    stage('Push to Dockerhub')
    {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        {
            app.push('latest')
        }
    }

    stage('Pull Image and Deploy')
    {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }

}
