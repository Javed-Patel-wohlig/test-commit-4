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

                        echo "reach here"
                        ls
                        cat count.txt
                    '''
                }
            }
        }
        stage('Update Count') {
            steps {
                    sh '''
                    commit_count=$(grep 'commit count is:' count.txt | awk '{print $NF}')
                    new_commit_count=$((commit_count + 50))
                    echo "hello i am devops" > count.txt
                    echo "my commit count is: $new_commit_count" >> count.txt
                    echo "thank you" >> count.txt
                    '''
            }
        }
        stage('Git pushing the update') {
            steps { 
                    sh '''
                        git add .
                        git commit -m "update new count"
                        git push origin main
                    '''
                }
        }
    }
}
