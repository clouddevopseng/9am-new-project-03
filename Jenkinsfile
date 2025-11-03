node {
    stage('Download') {
    git branch: 'dev', url: 'https://github.com/clouddevopseng/9am-new-project.git'
     }
    stage('Artifacts convert') {
    sh 'mvn package'
     }
    stage('Deploy into tomcat container') {
    deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '1cc14f2f-68cb-445b-9386-78522f0f5831', path: '', url: 'http://172.31.8.185:8080')], contextPath: '/business-application', war: '**/*.war'
     }  
}
