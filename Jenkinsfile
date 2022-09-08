pipeline{
  agent{
    node{
      label 'master'
      customWorkspace ('/mnt/projects/22Q2')
    }
  }
  stages{
    stage('permission given on slave'){
      agent{
        node{
          label 'slave-2'
        }
      }
      steps{
        /*sh "sudo mkdir /mnt/22Q2"*/
        sh "sudo chmod -R 777 /mnt/22Q2"
      }
    }
    stage('copy file to slave'){
      agent{
        node{
          label 'master'
        }
      }
      steps{
        sh "chmod -R 400 /mnt/projects/22Q2/23mayohio.pem"
        sh "scp -i 23mayohio.pem index.html ec2-user@172.31.41.127:/mnt/22Q2"
      }
    }
    stage('deploy on server'){
      agent{
        node{
          label 'slave-2'
        }
      }
      steps{
        sh "sudo yum install httpd -y"
        sh "sudo cp -r /mnt/22Q2/index.html /var/www/html/"
        sh "sudo chmod -R 777 /var/www/html/index.html"
        sh "sudo service httpd start"
      }
    }
  }
}
        
