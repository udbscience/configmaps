// create config maps based on branches
// filenames become config map names
// filter globals from CONFIG MAP

echo "branch:  ${env.BRANCH_NAME}"
def k8_cloud = 'dev'

podTemplate(label: 'jenkins-pipeline', containers: [
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.4.8', command: 'cat', ttyEnabled: true)
],
serviceAccount: 'cicd-jenkins',
volumes:[
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
]){
  node('jenkins-pipeline') {
      checkout scm
      container('kubectl') {
        sh "kubectl get nodes"
      }
  }
}
