pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
    stages {
      stage('Build'){
        steps {
          echo "Build step"
          sh 'mvn clean'
          sh 'mvn install'
          sh 'mvn package'
        }
        
      }
      stage('Test'){
        steps {
          echo "Test step"
          sh 'mvn test'
        }
        
      }
      stage('deploy'){
        steps {
          sshPublisher(publishers: [sshPublisherDesc(configName: 'docker-hosts', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'cd /home/dockeruser ; docker build -t devop_text . ; docker run -d --name jenkins_container -p 8080:8080 devop_text', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
        }
        
      }
      
        
    }
    post {
        always {
            echo "Always display this message"
        }
        failure {
            echo "Job failed"
        }
        success {
            echo "successful run"
        } 
        unstable {
            echo "The job is unstable"
        } 
    }
}
