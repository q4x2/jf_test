void setBuildStatus(String message, String state) {
step([
            $class: "GitHubCommitStatusSetter",
            reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/q4x2/jf_test"],
            statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
        ]);
    }

pipeline {
    stages {
        stage('Ask about approve') {
            steps {
                input(message: 'Approve PR?')
            }
        }
        stage ('Approve PR') {
            steps {
                        sh("echo true")
            }
        }
        stage('Ask about failure') {
            steps {
                input(message: "Let's fail?")
                error("oops")
          }
        }
    }
post {
    success {
        setBuildStatus("Build succeeded", "SUCCESS");
    }
    failure {
        sh("echo fail");
        setBuildStatus("Build failed", "SUCCESS");
    }
  }
}
