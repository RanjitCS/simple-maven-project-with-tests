pipeline {
      agent any

      stages {
          stage('Build & Test') {
              steps {
                  sh 'mvn clean jacoco:prepare-agent test jacoco:report -Dmaven.test.failure.ignore=true'
              }
          }

          stage('Coverage') {
              steps {
                  recordCoverage(
                      tools: [[parser: 'JACOCO']],
                      sourceCodeRetention: 'EVERY_BUILD',
                      qualityGates: [
                          [threshold: 80.0, metric: 'LINE', baseline: 'PROJECT', criticality: 'UNSTABLE'],
                          [threshold: 75.0, metric: 'BRANCH', baseline: 'PROJECT', criticality: 'UNSTABLE']
                      ]
                  )
              }
          }
      }
  }
