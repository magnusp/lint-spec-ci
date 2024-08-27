podTemplate(containers: [
    containerTemplate(name: 'spec-toolkit', image: 'ghcr.io/magnusp/specification-toolkit:5', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'spec-toolkit', image: 'ghcr.io/magnusp/specification-toolkit:5', command: 'cat', ttyEnabled: true),
  ]
  ) {
    node(POD_LABEL) {
        checkout scm

        stages {
            stage('The environment') {
                sh 'export'
            }
            stage('The stage') {
                when {
                    changeRequest
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
}
