#!/usr/bin/env groovy

def coverage_report_path = "covera"
/*
def publishHTMLReport(reportDir, file, reportName) {
  if (fileExists("${reportDir}/${file}")) {
    publishHTML(target: [
      allowMissing         : true,
      alwaysLinkToLastBuild: true,
      keepAll              : true,
      reportDir            : reportDir,
      reportFiles          : file,
      reportName           : reportName
    ])
  }
}
*/

node('master') {
  stage('checkout') {
    checkout scm
  }
  stage('NPM: Installing dependencies') {
    sh 'npm install'
  }
  stage('CODE QUALITY: ESLint') {
    sh 'npm run lint || exit 0'
    publishHTML(target: [
      allowMissing         : true,
      alwaysLinkToLastBuild: true,
      keepAll              : true,
      reportDir            : 'reports/eslint/',
      reportFiles          : 'index.html',
      reportName           : 'Code Quality: ESLint'
    ])
  }
  stage('CODE DUPLICASY: jscpd') {
    sh 'npm run cpd || exit 0'
    publishHTML(target: [
      allowMissing         : true,
      alwaysLinkToLastBuild: true,
      keepAll              : true,
      reportDir            : 'report/html/',
      reportFiles          : 'index.html',
      reportName           : 'Code Duplicasy: jscpd'
    ])
  }
  stage('BUG Scanning: OWASP Dependency-Check') {
    sh 'npm run owasp || exit 0'
    publishHTML(target: [
      allowMissing         : true,
      alwaysLinkToLastBuild: true,
      keepAll              : true,
      reportDir            : 'dependency-check-report/',
      reportFiles          : 'dependency-check-report.html',
      reportName           : 'Bug Scanning: OWASP'
    ])
  }
  stage('UNIT Testing: jest') {
    sh 'npm run test:unit || exit 0'
    publishHTML(target: [
      allowMissing         : true,
      alwaysLinkToLastBuild: true,
      keepAll              : true,
      reportDir            : 'coverage/',
      reportFiles          : 'index.html',
      reportName           : 'Unit Testing: Jest'
    ])
  }
  stage('INTEGRATION Testing: jest') {
    sh 'npm run test:integration || exit 0'
    publishHTML(target: [
      allowMissing         : true,
      alwaysLinkToLastBuild: true,
      keepAll              : true,
      reportDir            : 'coverage/',
      reportFiles          : 'index.html',
      reportName           : 'Integration Testing: Jest'
    ])
  }
}
