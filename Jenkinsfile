properties([
  pipelineTriggers([cron('H 23 * * *')]),
  disableConcurrentBuilds(),
  parameters([
    string(name: 'THREADS', defaultValue: '100'),
    string(name: 'DURATION', defaultValue: '300'),
    string(name: 'API_HOST', defaultValue: 'api-stage.santiment.net'),
  ])
])
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

        sh "jmeter -n -t wordContextTest.jmx -l wordContextTest.jtl -Jthreads ${params.THREADS} -Jduration ${params.DURATION} -Japi_host ${params.API_HOST}"
        archiveArtifacts(artifacts: 'wordContextTest.jtl', fingerprint: true)
      }
    }

    stage('Test Project By Slug') {
      container('jmeter') {
        sh "jmeter -n -t projectBySlugTest.jmx -l projectBySlugTest.jtl -Jthreads ${params.THREADS} -Jduration ${params.DURATION} -Japi_host ${params.API_HOST}"
        archiveArtifacts(artifacts: 'projectBySlugTest.jtl', fingerprint: true)
      }
    }

    stage('Test All Project Balances') {
      container('jmeter') {
        sh "jmeter -n -t allProjectsBalancesTest.jmx -l allProjectsBalancesTest.jtl -Jthreads ${params.THREADS} -Jduration ${params.DURATION} -Japi_host ${params.API_HOST}"
        archiveArtifacts(artifacts: 'allProjectsBalancesTest.jtl', fingerprint: true)
      }
    }

    stage('Generate Report') {
      container('jmeter') {
        perfReport(sourceDataFiles: "projectBySlugTest.jtl;wordContextTest.jtl;allProjectsBalancesTest.jtl")
      }
    }
  }
}
