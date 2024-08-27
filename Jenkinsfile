pipeline {
    agent {
        kubernetes {
            yaml '''
      spec:
        containers:
        - name: spec-toolkit
          image: ghcr.io/magnusp/specification-toolkit:5
          command: cat
          tty: true
        '''
        }
    }
    stages {
        stage('The environment') {
            steps {
                checkout scm
                sh 'export'
            }
        }
        stage('The stage') {
            when {
                changeRequest()
                changeset "openapi-spec.yaml"
            }
            steps {
                container('spec-toolkit') {
                    sh 'oasdiff --version'
                    sh 'vacuum version'
                }
            }
        }
    }
}
