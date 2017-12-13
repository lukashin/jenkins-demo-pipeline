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
        stage ('cdn verify') {
            steps {
                script {
                    def currentVersion = '2.2.11-117';
                    def previousVersion = '2.2.11-116';
                    def urls = http.download('https://raw.githubusercontent.com/lukashin/jenkins-demo-pipeline/master/cdn.urls')
                    println urls
                    urls.split().each {
                        http.verify(it, currentVersion, previousVersion)
                        println "${currentVersion} is present in ${it}"
                    }
                }
            }
        }
    }
}
