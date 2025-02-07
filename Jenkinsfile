node {
    try {
        stage('Build') {
            docker.image('python:3.12.1-alpine3.19').inside {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }

        stage('Test') {
            docker.image('qnib/pytest').inside {
                sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            junit 'test-reports/results.xml'
        }

        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk mengakhiri)'
        }

        stage('Deploy') {
            withEnv(["VOLUME=" + pwd() + "/sources:/src", "IMAGE=cdrx/pyinstaller-linux:python2"]) {
                dir(env.BUILD_ID) {
                    unstash(name: 'compiled-results')
                    sh "docker run --rm -v ${VOLUME} ${IMAGE} 'pyinstaller -F add2vals.py'"
                }
                archiveArtifacts "sources/dist/add2vals"
                sh "docker run --rm -v ${VOLUME} ${IMAGE} 'rm -rf build dist'"
            }
            sleep 60
        }
    } catch (Exception e) {
        // Handle exceptions or errors here
        currentBuild.result = 'FAILURE'
        throw e
    }
}
