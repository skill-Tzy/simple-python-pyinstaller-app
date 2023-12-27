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

        stage('Deliver') {
            withEnv(["VOLUME=" + pwd() + "/sources:/src", "IMAGE=cdrx/pyinstaller-linux:python2"]) {
                dir(env.BUILD_ID) {
                    unstash(name: 'compiled-results')
                    sh "docker run --rm -i -v ${VOLUME} ${IMAGE} pyinstaller --onefile /src/add2vals.py"
                }
                archiveArtifacts "${env.BUILD_ID}/sources/dist/add2vals"
                sh "docker run --rm -v ${VOLUME} ${IMAGE} rm -rf build dist"
            }
        }
    } catch (Exception e) {
        // Handle exceptions or errors here
        currentBuild.result = 'FAILURE'
        throw e
    }
}
