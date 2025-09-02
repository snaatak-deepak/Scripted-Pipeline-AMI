node {
    stage('Checkout') {
        // Checkout source code from GitHub
        checkout([$class: 'GitSCM',
                  branches: [[name: '*/main']],
                  userRemoteConfigs: [[url: 'https://github.com/snaatak-deepak/Scripted-Pipeline-AMI.git']]
        ])
    }

    stage('Validate Packer Template') {
        sh 'packer validate template.json'
    }

    stage('Build AMI') {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
                          credentialsId: 'aws-cred']]) {
            sh 'packer build template.json'
        }
    }
}
