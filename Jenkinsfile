pipeline{
  agent{
    node{
      label 'master'
      customWorkspace ('/mnt/projects/22Q1')
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
        sh "sudo chmod -R 777 /mnt"
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
        sh "scp -i 23mayohio.pem index.html ec2-user@172.31.38.178:/mnt/22Q1"
      }
    }
    stage('deploy on server'){
      agent{
        node{
          label 'slave-1'
        }
      }
      steps{
        sh "sudo yum install httpd -y"
        sh "sudo cp -r /mnt/22Q1/index.html /var/www/html/"
        sh "sudo chmod -R 777 /var/www/html/index.html"
        sh "sudo service httpd start"
      }
    }
  }
}
        
