pipeline 
{
    agent any
    
  
    stages 
    { 
        stage('Package')
        {
            steps
            {
                bat "mvn clean package"
            }
        }
        
        stage('Sonar Analysis')
        {
            steps
            {
                withSonarQubeEnv('SonarQube')
                {
                    bat 'mvn sonar:sonar'
                }
            }
        }
      
        stage('Jacoco report')
        {
            steps
            {
                jacoco()
            }
        }
         
        stage('Build Docker Image')
        {
            steps
            {
                script
                {
                    bat 'docker build -t sandeepchatuphale/test .'
                }
            }
        }
        
        
        /*stage('Pushing Docker Image Dockerhub')
        {
            steps
            {
                script
                {
                    withCredentials([string(credentialsId: 'sandeepchatuphale', variable: 'dockerhub')]) 
                    {
                        bat "docker login -u sandeepchatuphale -p ${dockerhub}"
                        bat 'docker push sandeepchatuphale/test'
                   }
                }
            }
         }*/
    }
}
