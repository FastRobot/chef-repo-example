#!groovy

pipeline {
  agent {
    docker {
      image 'chef/chefdk'
      // args '--rm'
    }
  }
  environment {
    // set $HOME so that chefdk puts gems in the right place
    HOME = '/tmp'
  }
  stages{
    stage('Compare') {
      steps {
        sh 'chef gem install knife-inspect'
        withCredentials([file(credentialsId: 'chefadmin.pem', variable: 'CHEFPEM')]) {
          sh 'knife inspect --no-cookbooks'
        }
      }
    }
    stage('Upload') {
      when { branch 'master' }
      steps {
        sh 'echo uploading'
          withCredentials([file(credentialsId: 'chefadmin.pem', variable: 'CHEFPEM')]) {
            sh '''
              berks install && berks upload
              knife upload /roles /data_bags /environments --chef-repo-path .
              '''
            }

      }
    }
    stage('Verify') {
      steps {
        sh 'echo testing'
      }
    }
  }
}

