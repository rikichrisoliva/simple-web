pipeline {
	agent any
	stages {
  stage('Setup') {
    steps {
      sh '''echo "Setting up ..."
      mkdir webapp
      cp -p /var/lib/jenkins/workspace/rikiwebapp-pipeline/index.py webapp
      cp -p /var/lib/jenkins/workspace/rikiwebapp-pipeline/Dockerfile webapp'''
    }
  }

  stage('Test') {
    steps {
      echo "Testing ..."
    }
  }

  stage('Deploy and Build') {
    steps {
      sshPublisher(publishers: [sshPublisherDesc(configName: 'docker-host-1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker build -t rikiwebapp-image .; sleep 10; docker run -d --name rikiwebapp-container -p5000:80 rikiwebapp-image;', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: 'webapp', sourceFiles: 'webapp/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
    }
  }

}

}