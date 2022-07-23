#!groovy

PROJECT_NAME = "mysql"
PROJECT_KEY = "tiggomark"
SCM = "GITHUB"

def repositoryUrl = 'thomazaudio'

node {


    def branch = "master"
    def environment = "prod"
    def tagVersion = "dev"

    stage(name: 'Checkout from SCM') {
        echo 'Checking out from scm'
        checkout scm
    }



    stage(name: 'Deploy to Docker Container') {
        echo 'Deploying images to docker container'
        //docker run --network cluster-network -p 8484:8484 --name customer-app -d customer-app:1.0.0
        sh "docker run --name database-app -d \
                -p 3307:3307 \
                --env MYSQL_ROOT_PASSWORD=leghacy150991 --env MYSQL_DATABASE=customer_app \
                --restart unless-stopped \
                --network cluster-network \
                mysql:5.7"
        echo "Deploy de ${PROJECT_NAME} para o ambiente ${environment} finalizado com sucesso"
        //sendMsgToSlack("Deploy de ${PROJECT_NAME} para o ambiente ${environment} finalizado com sucesso")
        //currentBuild.result = "SUCCESS"
    }

}



def sendMsgToSlack(text) {

/*
    try {
        build(job: "send-slack-message",
                parameters: [
                        string(name: "TITLE", value: "[${PROJECT_NAME}][${branch}]"),
                        string(name: "TITLELINK", value: env.BUILD_URL),
                        string(name: "TEXT", value: text),
                        string(name: "CHANNEL", value: "#podolsk-alerts")
                ]
        )
    } catch (all) {
        echo "Não foi possível enviar a mensagem para o canal #podolsk-alerts"
        echo "Error: ${all.message}"
    }
    */
}

def getVersion() {
    def lines = readFile("${env.WORKSPACE}/gradle.properties").split("\n")

    return lines.find { it.contains("version") }
            .split("=")[1]
            .trim()
}