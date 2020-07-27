/ This Jenkinsfile is an explame for multibranch pipeline

pipeline {
    agent none
    stages {
        stage("All platform builds") {
            parallel {
                stage("Windows build") {
                    agent {
                        node {
                            label 'windows-vm01'
                            customWorkspace 'C:\\agent\\workspace\\blog'
                        }
                    }
                    stages {
                        stage("PR build") {
                            when {
                                branch 'PR-*'
                            }
                            steps {
                                checkout scm
                                dir('src\\build') {
                                    bat label: '', script: 'build.bat PR'
                                }
                            }
                        }
                        stage("Release build") {
                            when {
                                branch 'develop'
                            }
                            steps {
                                cleanWs()
                                checkout scm
                                dir('src\\build') {
                                    bat label: '', script: 'build.bat release'
                                }
                            }
                        }
                        stage("Deploy") {
                            echo "====if you have more stage, can add stage like this==="
                        }
                    }
                }
                stage("Linux build") {
                    agent {
                        node {
                            label 'linux-vm01'
                            customWorkspace '/agent/workspace/blog'
                        }
                    }
                    stages {
                        stage("PR build") {
                            when {
                                branch 'PR-*'
                            }
                            steps {
                                checkout scm
                                dir('src/build') {
                                    bat label: '', script: 'build.sh PR'
                                }
                            }
                        }
                        stage("Release build") {
                            when {
                                branch 'develop'
                            }
                            steps {
                                cleanWs()
                                checkout scm
                                dir('src/build') {
                                    bat label: '', script: 'build.sh release'
                                }
                            }
                        }
                    }
                }
                stage("AIX build"){
                    steps{
                        echo "====same as windows/Linux example, can write the code here you need ===="
                    }
                }
            }
        }
    }
}
