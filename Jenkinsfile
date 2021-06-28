pipeline { 
    agent none 
    stages {
        stage('SCM_Chekout') {
            agent { label 'master'} 
            steps { 
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[url: 'https://github.com/ganeshhp/helloworldweb.git']]])
            }
        }
        stage('Build'){
            agent {label 'appserver'}
            steps {
                sh 'mvn -f pom.xml clean package' 
            }
        }
        stage('Deploy') {
            agent {label 'master'}
            steps {
                sh 'cp target/*.war /opt/tomcat/webapps/'
                sh '/opt/tomcat/bin/catalina.sh run'

            }
        }
    }
}
