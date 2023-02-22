pipeline{
    agent any
    triggers{
        cron: '* 18 * * 1-5'
    }
    stages{
        stage('Git clone'){
            steps{
                git branch: 'uat', url: 'https://github.com/virtualmail-rgb/spring-petclinic.git'  
                mail subject: 'Git clone is successfull',
                        body: 'Clonning is successful',
                        to  : 'virtualdevops@gmail.com'
            }
        }
        stage('build'){
            sh 'mvn clean package'
        } 
    }
    post {
        always {
            echo "job done or build copmleted"
            mail subject: 'Build completed for Jenkins JOB $env.JOB_NAME',
                body: 'for Jenkins JOB $env.JOB_NAME \n Click Here: $env.JOB_URL',
                to: "virtualdevops@gmail.com"
        }
        success {
            echo "Build is successfull"
            mail subject: 'for Jenkins JOB $env.JOB_NAME with Build ID $env.BUILD_ID',
                body: 'for Jenkins JOB $env.JOB_NAME',
                to: "virtualdevops@gmail.com"
        }
        failure {
            echo "Build is failed"
            mail subject: 'Build is failed Jenkins JOB $env.JOB_NAME with Build ID $env.BUILD_ID',
                body: 'Jenkins job is failed JOB $env.JOB_NAME',
                to: "virtualdevops@gmail.com"
        }
    }
}