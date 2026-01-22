pipeline {
    agent any

    stages {
        stage('Build & Test') {
            steps {
                sh 'mvn clean test -Dmaven.test.failure.ignore=true'
            }
        }

        stage('Coverage') {
            steps {
                // Explicitly specify the pattern and add additional configuration
                recordCoverage(
                    tools: [[parser: 'JACOCO', pattern: '**/target/site/jacoco/jacoco.xml']],
                    sourceCodeRetention: 'EVERY_BUILD',
                    sourceDirectories: [[path: 'src/main/java']],
                    qualityGates: [
                        [threshold: 80.0, metric: 'LINE', baseline: 'PROJECT', criticality: 'UNSTABLE'],
                        [threshold: 75.0, metric: 'BRANCH', baseline: 'PROJECT', criticality: 'UNSTABLE']
                    ]
                )
            }
        }
    }
}
