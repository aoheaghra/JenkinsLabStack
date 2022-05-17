
Jenkinsfile (Declarative Pipeline)

pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage ('checkout'){
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: scm.branches,
                    doGenerateSubmoduleConfigurations: false,
                    extensions: scm.extensions + [[$class: 'SubmoduleOption', disableSubmodules: false, recursiveSubmodules: true, reference: '', trackingSubmodules: false]],
                    submoduleCfg: [],
                    userRemoteConfigs: scm.userRemoteConfigs])
            }
        }
        stage ('build'){
            steps {
                sh 'make clean'
                sh 'make -j6 release'
            }
        }
        stage ('sonar-master'){
            when {
                branch 'master'
            }
            steps {
                sh "/opt/sonar-runner/bin/sonar-runner"
            }
        }
    }
}
