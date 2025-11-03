node {
    stage('Download') {
    git branch: 'test', url: 'https://github.com/clouddevopseng/9am-new-project.git'
     }
    stage('Artifacts convert') {
    sh 'mvn package'
     }
    stage('Deploy into tomcat container') {
    deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '688da7d5-53af-4485-adb8-76a4c381692d', path: '', url: 'http://172.31.13.134:8080')], contextPath: '/business-application-test', war: '**/*.war'
     }  
}
