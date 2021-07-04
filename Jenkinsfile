#!/usr/bin/env groovy

def coverage_report_path = "covera"

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


node('master') {
  stage('checkout') {
    checkout scm
  }
  stage('NPM: Installing dependencies') {
    sh 'npm install'
  }
  stage('CODE QUALITY: ESLint') {
    sh 'npm run lint || exit 0'
    publishHTMLReport('reports/eslint/', 'index.html', 'HTML Report')
  }
  stage('CODE DUPLICASY: jscpd') {
    sh 'npm run cpd || exit 0'
    publishHTMLReport('report/html/', 'index.html', 'HTML Report')
  }
  stage('BUG Scanning: OWASP Dependency-Check') {
    sh 'npm run owasp || exit 0'
    publishHTMLReport('dependency-check-report/', 'dependency-check-report.html', 'HTML Report')
  }
  stage('UNIT Testing: jest') {
    sh 'npm run test:unit || exit 0'
    publishHTMLReport('coverage/', 'index.html', 'HTML Report')
  }
  stage('INTEGRATION Testing: jest') {
    sh 'npm run test:integration || exit 0'
    publishHTMLReport('coverage/', 'index.html', 'HTML Report')
  }
}
