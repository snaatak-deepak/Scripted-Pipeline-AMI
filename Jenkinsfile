node {
    stage('Checkout') {
        // Checkout source code from GitHub
        checkout([$class: 'GitSCM',
                  branches: [[name: '*/main']],
                  userRemoteConfigs: [[url: 'https://github.com/snaatak-deepak/AMI.git']]
        ])
    }

    stage('Validate Packer Template') {
        sh 'packer validate ami.pkr.hcl'
    }

    stage('Build AMI') {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
                          credentialsId: 'aws-credentials']]) {
            sh 'packer build ami.pkr.hcl'
        }
    }
}
