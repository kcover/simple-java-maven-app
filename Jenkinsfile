//"Jenkins Pipeline is a suite of plugins which supports implementing and integrating continuous delivery pipelines into Jenkins. Pipeline provides an extensible set of tools for modeling delivery pipelines "as code" via the Pipeline DSL."
//More information can be found on the Jenkins Documentation page https://jenkins.io/doc/
pipeline {
    agent {
        node {
            label 'av-test'
            customWorkspace "/jenkins/workspace/${env.JOB_NAME}/${env.BUILD_NUMBER}"
        }
    }
     environment {
            WORKSPACE = "/jenkins/workspace/${env.JOB_NAME}/${env.BUILD_NUMBER}"
        }
    stages {
        stage('Build') {
            steps {
                    script {
                            sh 'mvn -B -DskipTests clean install'
                    }
            }
        }
        stage('Virus-Scan') {
          steps {
            script {
              sh 'freshclam && clamscan -r $WORKSPACE'
            }
          }
        }
    }
}
