def repo="https://github.com/Akhil-vellur/sample-helm-chart.git/"
pipeline {
  agent {
    kubernetes {
      label 'helm-pod'
      containerTemplate {
        name 'helm'
        image 'wardviaene/helm-s3'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run helm') {
      steps {
        container('helm')
                stage("add Repo") {
                        steps {
                               sh "helm repo add helm-test ${repo}"
                            }
                    }
				stage("Deploy to Dev") {
                        steps {
                            script{
					openshift.withCluster(){
                                        sh "helm upgrade --install helm-app Akhil-vellur/sample-app --values dev/values.yaml -n dev --wait"
                                    }
                                }
                            }
                    }
                stage("Deploy to UAT") {
                        steps {
                            script{
					openshift.withCluster(){
                                        sh "helm upgrade --install helm-app Akhil-vellur/sample-app --values uat/values.yaml -n uat --wait"
                                    }
                                }
                            }
                    }
            }
        }
