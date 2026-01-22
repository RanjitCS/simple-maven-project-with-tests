  pipeline {
      agent any

      stages {
          stage('Build & Test') {
              steps {
                  // Activate the coverage profile to generate JaCoCo reports
                  sh 'mvn clean test -Pcoverage -Dmaven.test.failure.ignore=true'
              }
          }

          stage('Coverage') {
              steps {
                  recordCoverage(
                      tools: [[parser: 'JACOCO']],
                      qualityGates: [
                          [threshold: 80.0, metric: 'LINE', baseline: 'PROJECT', criticality: 'UNSTABLE'],
                          [threshold: 75.0, metric: 'BRANCH', baseline: 'PROJECT', criticality: 'UNSTABLE']
                      ]
                  )
              }
          }
      }
  }
