node('docker'){
    stage('checkout'){
        echo "Checking the Git code"
        git brach: 'docker' credentialsId: 'lokigithubapikey', url: 'https://github.com/lokeshkamalay/simple-java-maven-app.git'
    }
    stage('Executing Test Cases'){
        docker.image('lokeshkamalay/batch2:maven').inside(){
            echo "Execuring Test Cases Started"
            sh "$mvnHome/bin/mvn clean test surefire-report:report-only"
            archiveArtifacts 'target/**/*'
            junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site', reportFiles: 'surefire-report.html', reportName: 'SureFireReportHTML', reportTitles: ''])
            echo "Executing Test Cases Completed"
        }
    }
    stage('Packaging'){
        echo "Preparing artifacts"
        sh "$mvnHome/bin/mvn package -DskipTests=true"
    }
}
