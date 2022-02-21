pipeline {
    agent any
        tools {
            maven "3.8.4"
                }
        stages {
            stage('Git Checkout'){
                steps {
                    git branch: 'main', credentialsId: 'Demo-Project01', url: 'https://github.com/dharmendra3671/Demo-Project01'
                }
            }
        stage ('Python') {
            steps {
                bat 'PythonwithJson.py'
            }
        }

        stage ('Server'){
            steps {
                rtServer (
                    id: "Artifactory",
                    url: 'http://127.0.0.1:8082/artifactory',
                    username: 'admin',
                    password: 'Indro@6805',
                    bypassProxy: true,
                    timeout: 300
                        )

            }
        }
        stage ('Upload'){
            steps{
                rtUplode (
                 serverId:"Artifactory",
                  spec: '''{
                   "files": [
                      {
                      "pattern": ".zip",
                      "target": "Zipfile_artifact"
                      }
                            ]
                           }''',
                        )
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "Artifactory"
                )
            }
        }
    }
}       
