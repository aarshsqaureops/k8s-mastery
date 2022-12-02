pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
          - name: docker
            image: docker:latest
            command:
            - cat
            tty: true
            volumeMounts:
             - mountPath: /var/run/docker.sock
               name: docker-sock
          volumes:
          - name: docker-sock
            hostPath:
              path: /var/run/docker.sock
        '''
    }
  }
  stages {
    stage('Clone') {
      steps {
        container('maven') {
          git branch: 'master', changelog: false, poll: false, url: 'https://github.com/aarshsqaureops/k8s-mastery.git'
        }
      }
    }
	stage('Build-Docker-Image') {
      steps {
        container('docker') {
		  script{
          echo "Test code from github"
          sh  '''
          echo "dckr_pat_gllAO-xQXrEgBUchziw0wXcxHoY"| docker login --username aarshsquareops --password-stdin
          cd sa-frontend
          #docker build -t frontapp .
          #docker tag frontapp aarshsquareops/frontapp-test:latest-${BUILD_NUMBER}
          #docker push aarshsquareops/frontapp-test:latest-${BUILD_NUMBER}
          #cd ../sa-logic/
          #docker build -t logicapp .
          #docker tag logicapp aarshsquareops/logicapp-test:latest-${BUILD_NUMBER}
          #docker push aarshsquareops/logicapp-test:latest-${BUILD_NUMBER}
          cd ../sa-webapp/
          docker build -t webapp .
          docker tag webapp aarshsquareops/webapp-test:latest-${BUILD_NUMBER}
          docker push aarshsquareops/webapp-test:latest-${BUILD_NUMBER}
          '''
        }
        }
      }
    }
  }
  }
