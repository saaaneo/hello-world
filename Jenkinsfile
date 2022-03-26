pipeline {
    agent any

    stages {
        stage('Preparation') {
            steps {
                git branch: 'pipeline', url: 'https://github.com/saaaneo/hello-world.git'
            }
        }
		stage('Build') {
            steps {
                sh "mvn -f pom.xml clean install package"
            }
        }
		post {
				always {
					sshPublisher(publishers: [sshPublisherDesc(configName: 'docker_host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker stop hello_world; docker rm -f hello_world; docker image rm -f hello_world; cd /opt/docker; docker build -t hello_world .', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false), sshPublisherDesc(configName: 'docker_host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker run -d --name hello_world -p 8090:8080 hello_world', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
				}
				failure {
					mail to: aalhad.vengurlekar@neosoftmail.com , subject: 'The helloworld-docker Pipeline failed :('
				}
			}
    }
}
