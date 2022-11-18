pipeline{
agent any
  environment{
    Image_Repo="aarshsquareops"
    Branch="master"
    Docker_Cred=credentials('dockerhub')
    //Github_Cred=credentials('github')
  }
stages{
  stage('Go to repo'){
    steps{
      //container('dind'){ 
        script{
          echo "take code from github"
          git branch: 'master',
                credentialsId: 'github',
                url: 'https://github.com/aarshsqaureops/k8s-mastery.git'
           //sh  '''
             // git clone -b $Branch https://github.com/aarshsquareops/k8s-mastery.git
             //'''
             echo "Branch copied"
        }
      //}
    }
  } 
  stage('Build Image and push to dockerhub'){
    steps{
      //container('docker'){
        script{
          echo "Test code from github"
          sh  ''' 
          echo "dckr_pat_gllAO-xQXrEgBUchziw0wXcxHoY"| docker login --username aarshsquareops --password-stdin
          cd sa-frontend
          docker build -t frontapp .
          docker tag frontapp $Image_Repo/frontapp:latest-${BUILD_NUMBER}
          docker push $Image_Repo/frontapp:latest-${BUILD_NUMBER}
          #cd ../sa-logic/
          #docker build -t logicapp .
          #docker tag logicapp $Image_Repo/logicapp:latest-${BUILD_NUMBER}
          #docker push $Image_Repo/logicapp:latest-${BUILD_NUMBER}
          cd ../sa-webapp/
          docker build -t webapp .
          docker tag webapp $Image_Repo/webapp:latest-${BUILD_NUMBER}
          docker push $Image_Repo/webapp:latest-${BUILD_NUMBER}
          '''
        }
      //}
    }
  }
  
  }
  }
