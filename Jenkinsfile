node('master') {
   ws('/disk/docker/dockprom') {
      stage('Git checkout') {
         ansiColor('xterm') {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'LocalBranch', localBranch: 'master']], submoduleCfg: [], userRemoteConfigs: [[url: 'git@github.com:Tibi02/dockprom.git']]])
         }
      }
   
      stage('Compose pull') {
         ansiColor('xterm') {
            sh('docker-compose pull')
         }
      }
   
      stage('Compose up') {
         ansiColor('xterm') {
            withCredentials([usernamePassword(credentialsId: 'grafana-user', passwordVariable: 'ADMIN_PASSWORD', usernameVariable: 'ADMIN_USER')]) {
               sh('COMPOSE_PROJECT_NAME=dockprom docker-compose up -d --force-recreate')
            }
         }
      }
   }
}
