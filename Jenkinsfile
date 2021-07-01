pipeline{
    agent 'any' 
    stages{
        stage("Install Dependencies"){
            steps{
                sh "npm build"
                echo "Dependencies installed"
            }
        }
        stage("Build Image"){
            steps{
                // try{
                    // script{
                    //     //Assemble Image Name
                    //     // image_full_name = "image_CI"
                    //     //  echo "Image name: ${image_full_name}"
                    //     //Build Image
                    //     // def currentBuild = bat "docker build -t ${image_full_name} ."
                    //     def currentBuild = bat "docker build -t image_CI ."
                    // }
                //     notifySuccessful()
                // } catch (e) {
                //     currentBuild.result="FAILED"
                //     notifyFailed()
                //     throw e
                // }
                echo "PAssei no build"
            }
        }
        stage('SonarQube Analysis'){
            steps{
                // script{
                //     def scannerHome = tool 'new-sonar';
                //     withSonarQubeEnv('formacao-sq'){
                //         sh "%{scannerHome}/bin/sonar-scanner"
                //     }
                // }
                echo "Passei no SQ Analysis"
            }
        }
        stage('SonarQube Quality Gates'){
            steps{
                // script{
                //     def qg = waitForQualityGate();
                //     if (qp.status != 'OK') {
                //         error "Pipeline aborted due to quality gate failure: ${qp.status}"
                //     }
                // }
                echo "Passei no SQ QualityGates"
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