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

        sh "jmeter -n -t wordContextTest.jmx -l result.jtl -Jthreads 100 -Jduration 300"
        archiveArtifacts(artifacts: 'result.jtl', fingerprint: true)
        perfReport("result.jtl")
      }
    }

    stage('Test Project By Slug') {
      container('jmeter') {
        def scmVars = checkout scm

        sh "jmeter -n -t projectBySlug.jmx -l result.jtl -Jthreads 10 -Jduration 300"
        archiveArtifacts(artifacts: 'result.jtl', fingerprint: true)
        perfReport("result.jtl")
      }
    }
  }
}