pipeline{
    stages{
        stage("Install Dependencies"){
            steps{
                sh "npm build"
                echo "Dependencies installed"
            }
        }
        stage("Build Image"){
            steps{
                try{
                    script{
                        //Assemble Image Name
                        image_full_name = "image_CI"
                         echo "Image name: ${image_full_name}"
                        //Build Image
                        def currentBuild = bat "docker build -t ${image_full_name} ."
                    }
                    notifySuccessful()
                } catch (e) {
                    currentBuild.result="FAILED"
                    notifyFailed()
                    throw e
                }
            }
        }
        stage('SonarQube Analysis'){
            setps{
                scripts{
                    def scannerHome = tool 'new-sonar';
                    withSonarQubeEnv('formacao-sq'){
                        sh "%{scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        stage('SonarQube Quality Gates'){
            setps{
                scripts{
                    def qg = waitForQualityGate();
                    if (qp.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qp.status}"
                    }
                }
            }
        }
    }
    post{
        always{
            echo "Delete Dir"
            deleteDir()
        }
        success{
            echo "Pipeline ends with SUCCESS"
        }
        failure{
            echo "Pipeline with fails"
        }
    }
}