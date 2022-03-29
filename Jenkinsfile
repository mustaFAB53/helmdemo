node {
    def version
    // stage('Checkout Github Repo') {
    //     git 'https://github.com/mustaFAB53/helmdemo.git'
    // }
    stage('Helm Lint') {
        sh "helm lint helmcharts/sample-chart/"
    }
    stage('Helm Dependency Update') {
        sh "helm dependency update helmcharts/sample-chart/"
    }
    stage('Helm Package') {
        version = "0.${BUILD_NUMBER}.0"
        sh "helm package helmcharts/sample-chart/ --version $version"
    }
    stage('Install Helm Chart'){
        withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
            sh "helm upgrade --install myhelm sample-chart-${version}.tgz"
        }
    }
}
