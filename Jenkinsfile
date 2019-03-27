podTemplate(label: 'performace_tests', containers: [
  containerTemplate(
    name: 'jmeter',
    image: 'justb4/jmeter',
    command: '/bin/sh -c "tail -f /dev/null"'
  )
]) {
  node('performace_tests') {
    stage('Test Word Context') {
      container('jmeter') {
        def scmVars = checkout scm

        sh "ls -l"
        sh "jmeter -n -t wordContextTest.jmx -e -o results -l result.jtl -Jthreads 10 -Jduration 300"
        archiveArtifacts(artifacts: 'results/**', fingerprint: true)
        archiveArtifacts(artifacts: 'result.jtl', fingerprint: true)
        perfReport 'result.jtl'
      }
    }
  }
}