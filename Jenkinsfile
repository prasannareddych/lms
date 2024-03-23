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
        stage('LMS-build'){
            steps{
                echo 'build started'
                sh 'cd webapp && npm install && npm run build'
                echo 'build completed'
            }
        }
        stage('LMS-publish'){
            steps{
                echo 'publish started'
                def packageJSON = readJSON file: 'webapp/package.json'
                def packageJSONVersion = packageJSON.version
                echo "${packageJSONVersion}"
                sh "zip webapp/lms-${packageJSONVersion}.zip -r webapp/dist"
                sh "curl -v -u admin:t8LS2rs6btQz --upload-file lms-${packageJSONVersion}.zip https://nexus.chspr.in/repository/lms/"   
                echo 'build completed'
            }
        }
    }
}
