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

        sh "jmeter -n -t wordContextTest.jmx -l wordContextTest.jtl -Jthreads 100 -Jduration 300"
        archiveArtifacts(artifacts: 'wordContextTest.jtl', fingerprint: true)
      }
    }

    stage('Test Project By Slug') {
      container('jmeter') {
        sh "jmeter -n -t projectBySlugTest.jmx -l projectBySlugTest.jtl -Jthreads 20 -Jduration 300"
        archiveArtifacts(artifacts: 'projectBySlugTest.jtl', fingerprint: true)
      }
    }

    stage('Generate Report') {
      container('jmeter') {
        perfReport(sourceDataFiles: "projectBySlugTest.jtl;wordContextTest.jtl")
      }
    }
  }
}