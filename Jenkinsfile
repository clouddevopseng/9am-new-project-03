node {
   try {
    stage('Download') {
    git branch: 'test', url: 'https://github.com/clouddevopseng/9am-new-project.git'
     }
    stage('Artifacts convert') {
    sh 'mvn package'
     }

     // If everything looks good success
     emailext(
         subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
	 body: """<p> The jenkins build success ${env.JOB_NAME} #${env.BUILD_NU         MBER}</p>
	 to: 'venkata.palakeela@gmail.com'
	 )
     } catch (Exception e) {
     // If Failed
     emailext(
          subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
         body: """<p> The jenkins build success ${env.JOB_NAME} #${env.BUILD_NU         MBER</p>
	 <p>Error: $(e.getMessage()}</p>
         to: 'venkata.palakeela@gmail.com'
         )
	 throw e

     }

    stage('Deploy into tomcat container') {
    deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '688da7d5-53af-4485-adb8-76a4c381692d', path: '', url: 'http://172.31.13.134:8080')], contextPath: '/business-application-test', war: '**/*.war'
     }  
}
