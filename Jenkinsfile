pipeline {
  agent any
  stages {
    stage('initial_setup') {
      steps {
        sh '''cd android
        fastlane gradle_clean_bridge'''
      }
    }
    stage('node_modules (clean install)') {
      steps {
        sh '''cd Examples
        rm -rf node_modules ; npm install'''
      }
    }
    stage('viroreact (android)') {
      steps {
        sh '''cd android
        fastlane react_viro_bridge_aar'''
      }
    }
    stage('viroreact (iOS)') {
      steps {
        sh '''cd Examples/ios
        fastlane release_react_viro_lib'''
      }
    }
    stage('npm_pack') {
      steps {
        sh '''cd Examples/android
        fastlane npm_pack'''
      }
    }
/*    stage('release_tests (iOS)') {
      steps {
        sh '''cd Examples/ios
fastlane jenkins_release_tests'''
      }
    }
    stage('upload_to_testflight') {
      steps {
        sh '''cd Examples/ios
fastlane jenkins_upload_release_tests_testflight'''
      }
    }
*/
    stage('release_tests (android)(gvr+ovr)') {
      steps {
        sh '''cd Examples/android/
        fastlane gvr_release_test
        fastlane ovr_release_test'''
      }
    }
    stage('upload_to_s3_slack') {
      steps {
        sh '''cd android/
        fastlane upload_builds_and_slack'''
      }
    }
  }
  environment {
    LC_ALL = 'en_US.UTF-8'
    LANG = 'en_US.UTF-8'
  }
}
