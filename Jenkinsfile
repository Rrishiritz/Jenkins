pipeline {
    agent any
    parameters {
         string(name: 'tomcat_staging', defaultValue: '54.153.121.139', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '13.57.204.205', description: 'Production Server')
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving starts here...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging environment'){
                    steps {
                        sh "echo y | pscp -i C:\\Users\\grvtr\\Desktop\\Project\\AlternativeFiles\\Redis-Key.ppk C:\\Users\\grvtr\\Desktop\\Project\\AlternativeFiles\\*.war ec2-user@${params.tomcat_staging}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production environment"){
                    steps {
                        sh "echo y | pscp -i C:\\Users\\grvtr\\Desktop\\Project\\AlternativeFiles\\Redis-Key.ppk C:\\Users\\grvtr\\Desktop\\Project\\AlternativeFiles\\*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}
