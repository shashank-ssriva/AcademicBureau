node {
    stage('Package') {  
      xldCreatePackage artifactsPath: '/', darPath: 'AcademicBureau-${BUILD_NUMBER}.dar', manifestPath: 'deployit-manifest.xml'
      }
    stage('Push to Nexus') {  
      nexusArtifactUploader artifacts: [[artifactId: 'AcademicBureau', classifier: '', file: 'AcademicBureau-${BUILD_NUMBER}.war', type: 'war']], credentialsId: 'nexus-admin-user', groupId: 'AcademicBureau', nexusUrl: 'localhost:8083', nexusVersion: 'nexus3', protocol: 'http', repository: 'war-pipeline-repo', version: '${BUILD_NUMBER}'
      }
    stage('Publish') {
      xldPublishPackage darPath: 'AcademicBureau-${BUILD_NUMBER}.dar', serverCredentials: 'Prod XLD'
      }
    stage('Deploy') {
      xldDeploy environmentId: 'Environments/Tomcat9', packageId: 'Applications/AcademicBureau-Pipeline', serverCredentials: 'Prod XLD'
      }
}
