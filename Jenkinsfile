    // Pod Template
def podLabel = "nw-app-fil-si"
def cloud = env.CLOUD ?: "kubernetes"
def registryCredsID = env.REGISTRY_CREDENTIALS ?: "registry-credentials-id"
def dockerHubCredsID = env.DOCKER_HUB_CREDENTIALS ?: "docker-hub-credentials-id"
def serviceAccount = env.SERVICE_ACCOUNT ?: "jenkins"

// Pod Environment Variables
def namespace = env.NAMESPACE ?: "default"
def targetNamespace = env.TARGET_NAMESPACE ?: "nw-app-fil-si-dev"
def registry = env.REGISTRY ?: "mycluster.icp"
def registryIP = env.REGISTRY_IP ?: "10.187.162.3"
def imageNameMQ = env.IMAGE_NAME_MQ ?: "mq9-nw-fildvqm"
def imageNameApp1 = env.IMAGE_NAME_APP1 ?: "fil-si-filemonitor-ear"
def imageNameApp2 = env.IMAGE_NAME_APP2 ?: "fil-si-dispatcher-ear"
def imageNameApp3 = env.IMAGE_NAME_APP3 ?: "fil-si-res-dispatcher-ear"
def imageNameApp4 = env.IMAGE_NAME_APP4 ?: "fil-si-web-ear"
def statefulSet = env.STATEFUL_SET ?: "nw-app-fil-si"
def deploymentLabels = env.DEPLOYMENT_LABELS ?: "app=nw-app-fil-si"
def podName = env.POD_NAME ?: "nw-app-fil-si"


podTemplate(label: podLabel, cloud: cloud, serviceAccount: serviceAccount, namespace: namespace, envVars: [
        envVar(key: 'NAMESPACE', value: namespace),
        envVar(key: 'TARGET_NAMESPACE', value: targetNamespace),
        envVar(key: 'REGISTRY', value: registry),
        envVar(key: 'REGISTRY_IP', value: registryIP),
        envVar(key: 'IMAGE_NAME_MQ', value: imageNameMQ),
        envVar(key: 'IMAGE_NAME_APP1', value: imageNameApp1),
        envVar(key: 'IMAGE_NAME_APP2', value: imageNameApp2),
        envVar(key: 'IMAGE_NAME_APP3', value: imageNameApp3),
        envVar(key: 'IMAGE_NAME_APP4', value: imageNameApp4),
        envVar(key: 'STATEFUL_SET', value: statefulSet),
        envVar(key: 'DEPLOYMENT_LABELS', value: deploymentLabels),
        envVar(key: 'POD_NAME', value: podName)
    ],
    volumes: [
        emptyDirVolume(mountPath: '/var/lib/docker', memory: false)
    ],
    containers: [
        containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl', ttyEnabled: true, command: 'cat'),
        containerTemplate(name: 'docker', image: 'ibmcase/docker:18.09-dind', privileged: true)
  ]) {

    node(podLabel) {
        checkout scm
        container('docker') {

            stage('Aqua Microscanner') {
                aquaMicroscanner imageName: 'mapit/mapit-dev', notCompliesCmd: 'exit 4', onDisallowed: 'fail', outputFormat: 'html'
            }
        }
    }
}