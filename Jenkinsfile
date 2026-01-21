  pipeline {
      agent any  // Uses any available agent

      stages {
          stage('Build & Test') {
              steps {
                  sh 'mvn clean test'
              }
          }

          stage('Coverage') {
              steps {
                  recordCoverage(
                      tools: [[parser: 'JACOCO']],
                      qualityGates: [
                          [threshold: 80.0, metric: 'LINE', baseline: 'PROJECT', unstable: true],
                          [threshold: 75.0, metric: 'BRANCH', baseline: 'PROJECT', unstable: true]
                      ]
                  )
              }
          }
      }
  }
