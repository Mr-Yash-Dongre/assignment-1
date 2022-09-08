pipeline{
  agent{
    node{
      label 'master'
      customWorkspace ('/mnt/projects')
    }
  }
  stages{
    stage('permission given on slave'){
      agent{
        node{
          label 'slave-1'
        }
      }
      steps{
        sh "chmod -R 777 /mnt"
      }
    }
    stage('copy file to slave-1'){
      agent{
        node{
          label 'master'
        }
      }
      steps{
        sh "chmod -R 400 23mayohio.pem"
        sh "scp -i 23mayohio.pem index.html ec2-user@172.31.38.178:/mnt"
      }
    }
    stage('deploy on server'){
      agent{
        node{
          label 'slave-1'
        }
      }
      steps{
        sh "cp -r /mnt/index.html /var/www/html"
        sh "chmod -R /var/www/html/index.html"
      }
    }
  }
}
        
