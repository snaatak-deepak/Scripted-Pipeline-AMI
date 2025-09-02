node {
    stage('Checkout') {
        // Checkout source code from GitHub
        checkout([$class: 'GitSCM',
                  branches: [[name: '*/main']],
                  userRemoteConfigs: [[url: 'https://github.com/snaatak-deepak/Scripted-Pipeline-AMI.git']]
        ])
    }

    stage('Validate Packer Template') {
        echo "Validating Packer template..."
        sh 'packer validate template.json'
    }

    stage('Build AMI') {
        echo "Building AMI with Packer..."
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
                          credentialsId: 'aws-cred']]) {
            sh '''
                export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
                export AWS_DEFAULT_REGION=ap-south-1
                packer build template.json
            '''
        }
    }
}
