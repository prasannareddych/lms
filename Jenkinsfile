pipeline{
    agent any
    stages{
        stage('LMS-sonar-scan'){
            steps{
                echo 'sonar scan started'
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="https://sonarqube.chspr.in" -e SONAR_LOGIN="sqp_50f07cee0d04341a235a383c8c677a9381ad7cac"  -v ".:/usr/src" david1155/sonar-scanner-cli:5 -Dsonar.projectKey=lms'
                echo 'sonar scan completed'
            }
        }
    }
}
