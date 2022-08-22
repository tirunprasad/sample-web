node(){
    
    def mavenHome = tool name: "maven 3.8.4"
    
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'RebuildSettings', autoRebuild: false, rebuildDisabled: false], [$class: 'JobLocalConfiguration', changeReasonComment: '']])
    
    stage('GetCode'){
        git branch: 'main', url: 'https://github.com/tirunprasad/sample-web.git'
    }
    
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    
    stage('ExecuteSonar'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
    stage('Deploy'){
        sshagent(['82c93a75-e757-4dfc-8b89-3cbe358c2c72']) {
    
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.127.254.49:/opt/apache-tomcat-9.0.65/webapps/"
}
    }
    stage('sendEmial'){
        emailext body: '''BuilldOver......

Regards
YourSon''', subject: 'BuildOver', to: 'vizagprasad9@gmail.com'
    }
    
}
