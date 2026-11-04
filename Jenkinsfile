@Library('jenkins-shared-library') _

properties([
  parameters([
    string(name: 'appVersion', defaultValue: ''),
    string(name: 'deploy_to', defaultValue: 'dev')
  ])
])

def configmap = [
    project: "roboshop",
    component: "catalogue",
    APP_VERSION: (params.APP_VERSION),
    deploy_to: (params.deploy_to)
]

EKSDeploy(configmap)
