pipeline {
    agent any
    parameters {
        string(name: "tomcat_dev", defaultValue: "3.80.62.15", description: "Staging server")
        string(name: "tomcat_prod", defaultValue: "54.89.230.183", description: "Production server")
    }
    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i C:/Users/arnoldrx/Downloads/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i C:/Users/arnoldrx/Downloads/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}