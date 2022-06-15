pipeline{
    agent any
    tools {
        maven 'MavenForApp1'
    }

    stages{
        stage("Test"){
            steps{
                //echo "test"
                sh 'mvn test'
            }
            
        }
        stage("Build"){
            steps{
                //echo "Build"
                sh 'mvn install'
            }
            
        }
        stage("Deply on test"){
            steps{

                deploy adapters: [tomcat9(credentialsId: 'testtom', path: '', url: 'http://192.168.122.36:8080/app_abhay')], contextPath: 'app_abhay', war: '**/*.war'
            }
            
        }
        stage("Deploy on Prod"){
            input {
                message 'You want to Continue'
            }
            steps{

                deploy adapters: [tomcat9(credentialsId: 'prodtom', path: '', url: 'http://192.168.122.35:8080/app_abhay')], contextPath: 'app_abhay', war: '**/*.war'
            }
            
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "sucess"
        }
        failure{
            echo "Failed"
        }
    }
}
