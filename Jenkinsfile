import groovy.json.JsonSlurper

def getSource() {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '6a091ff4-16c1-4bdb-a8ea-fadf63c78d7a', url: 'http://gitlab.w55.ru/dzorenko/day10.git']]])
}

def parseData() {
    def json = "${env.data}"
    def slurped = new JsonSlurper().parseText(json)
    for (int i=0; i<slurped.members.size(); i++)
    println("Name: " + slurped.members[i].name + "\nAge: " + slurped.members[i].age)
}

def parseIP() {
    def response = httpRequest 'https://ifconfig.me/all.json'
    def jsonOBJ = new JsonSlurper().parseText(response.content)
    println("IP: " +jsonOBJ.ip_addr)
}

node() {
timestamps {
	try {
		stage("Getting source code") {
			getSource()
		}
		stage("Parsing data") {
            parseData()
        }
        stage("Parsing data") {
            parseIP()
        }
	} catch (Exception ex) {
		println(ex)
		currentBuild.result = 'FAILURE'
	} finally {
		cleanWs()
	}
}
}