pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/kimhj4270/jen.git', branch: 'main'
      }
    }
    stage('docker build') {
      steps {
        sh '''
        sudo docker build -t 192.168.0.151:5000/mynginx:latest .
        sudo docker push 192.168.0.151:5000/mynginx:latest
        '''
      }
    }
    
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl delete -f web-pod.yml
        sleep 10
        sudo kubectl apply -f web-pod.yml
        '''
      }
    }
    
  }
}
