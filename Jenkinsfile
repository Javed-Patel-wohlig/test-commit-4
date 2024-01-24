pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                git url:"https://github.com/Javed-Patel-wohlig/test-gitops", branch:"main"
            }
        }

        stage('Configuration of Github') {
            steps {
                script {
                    sh '''
                        git config --global user.email "javed.patel@wohlig.com"
                        git config --global user.name "Javed-Patel-wohlig"
                    '''
                }
            }
        }

        stage('Update Count') {
            steps {
                script {
                    dir('test-gitops') {
                        def commit_count = sh(script: "grep -oE '(commit count is: )([0-9]+)' count.txt | cut -d' ' -f4", returnStdout: true).trim()
                        def new_commit_count = commit_count.toInteger() + 50

                        sh "sed -i 's/my commit count is: [0-9]+/my commit count is: ${new_commit_count}/' count.txt"
                    }
                }
            }
        }

        stage('Git pushing the update') {
            steps {
                script {
                    dir('test-gitops') {
                        sh '''
                            git add .
                            git commit -m "update new count"
                            git push origin main
                        '''
                    }
                }
            }
        }
    }
}
