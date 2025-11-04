node {
    try {
        stage('Download') {
            git branch: 'test', url: 'https://github.com/clouddevopseng/9am-new-project.git'
        }
        
        stage('Artifacts convert') {
            sh 'mvn package'
        }

        // Success Email
        stage('Send Success Email') {
            emailext(
                subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>The Jenkins build was successful: <b>${env.JOB_NAME}</b> #${env.BUILD_NUMBER}</p>
                         <p>Check console output at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
                to: 'venkata.palakeela@gmail.com',
                mimeType: 'text/html'
            )
        }

        // Deploy only if previous stages succeed
        stage('Deploy into tomcat container') {
            deploy adapters: [tomcat9(
                credentialsId: '688da7d5-53af-4485-adb8-76a4c381692d',
                path: '',
                url: 'http://172.31.13.134:8080'
            )],
            contextPath: '/business-application-test',
            war: '**/*.war'
        }

    } catch (Exception e) {
        // Failure Email
        emailext(
            subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """<p>The Jenkins build failed: <b>${env.JOB_NAME}</b> #${env.BUILD_NUMBER}</p>
                     <p>Error: ${e.getMessage()}</p>
                     <p>Check console output at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
            to: 'venkata.palakeela@gmail.com',
            mimeType: 'text/html'
        )
        throw e  // Re-throw to mark build as failed
    }
}

