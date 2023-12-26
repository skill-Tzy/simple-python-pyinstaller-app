node {
    options {
        skipStagesAfterUnstable()
    }

    stage('Build') {
        def dockerImage = 'python:3.12.1-alpine3.19'
        checkout scm
        docker.image(dockerImage).inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            stash(name: 'compiled-results', includes: 'sources/*.py*')
        }
    }

    stage('Test') {
        def dockerImage = 'qnib/pytest'
        checkout scm
        docker.image(dockerImage).inside {
            sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
        }
        post {
            always {
                junit 'test-reports/results.xml'
            }
        }
    }

    stage('Deliver') {
        def dockerImage = 'cdrx/pyinstaller-linux:python2'
        def volume = "${pwd()}/sources:/src"

        agent any
        environment {
            VOLUME = volume
            IMAGE = dockerImage
        }

        steps {
            dir(path: env.BUILD_ID) {
                unstash(name: 'compiled-results')
                sh "docker run --rm -v ${VOLUME} ${IMAGE} 'pyinstaller -F add2vals.py'"
            }
        }

        post {
            success {
                archiveArtifacts "${env.BUILD_ID}/sources/dist/add2vals"
                sh "docker run --rm -v ${VOLUME} ${IMAGE} 'rm -rf build dist'"
            }
        }
    }
}
