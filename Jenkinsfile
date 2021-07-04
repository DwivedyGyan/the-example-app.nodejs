#!/usr/bin/env groovy

node('master') {
  stage('checkout') {
    checkout scm
  }
  stage('NPM: Installing dependencies') {
    sh 'npm install'
  }
  stage('CODE QUALITY: ESLint') {
    sh 'npm run lint'
  }
  stage('CODE DUPLICASY: jscpd') {
    sh 'npm run cpd'
  }
  stage('BUG Scanning: OWASP Dependency-Check') {
    sh 'npm run owasp'
  }
}
