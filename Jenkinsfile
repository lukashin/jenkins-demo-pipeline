

pipeline {
    agent {
        label "master"
    }
    stages{
        stage ('HI!') {
            steps{
                script {
                    println pr.labels(1)
                    if (pr.hasLabel(1, "enhancement")) {
                        manager.addShortText("enhancement", "white", "blue", "1px", "blue")
                    }
                }
                echo "hi there!"
            }
        }
        stage ('conditional (question)') {
            when { 
                expression { 
                    pr.hasLabel(1, "question")   
                }
            }
            steps{
                script {
                    manager.addShortText("question", "white", "magenta", "1px", "magenta")
                }
                echo "confiditional - only if PR has question label: question"
            }
        }
        stage ('conditional (help wanted)') {
            when { 
                expression { 
                    pr.hasLabel(1, "help wanted")   
                }
            }
            steps{
                echo "confiditional - only if PR has question label: help wanted!"
                script {
                    manager.addShortText("help wanted", "white", "green", "1px", "green")
                }
            }
        }
        stage ('translations') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'cad5438e-62f0-4e70-bcdd-e51891bc2b8b', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    echo "I'm user = ${USER}"
                }
                script {
                    updateTranslations(['en', 'de', 'it'])
                }
            }
        }
    }
}
