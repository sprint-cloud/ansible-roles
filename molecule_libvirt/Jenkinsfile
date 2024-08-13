def scenarios = [
    "master" : ["ubuntu", "centos", "ubuntu-same-1804", "ubuntu-same-2004"],
    "Agent-1": ["ubuntu-same-2110", "ubuntu-same-2204", "centos-same-7", "centos-same-8", "centos-same-9"],
]

def nodes = [:]

for (kv in mapToList(scenarios)) {
    def nodeName = kv[0]
    def scenarioList = kv[1]

    nodes[nodeName] = {
        node("${nodeName}") {
            stage("Checkout") {
                checkout scm
            }

            for(int i = 0; i < scenarioList.size(); i++) {
                stage("${scenarioList[i]}") {
                    withEnv([
                    'HYPERVISOR_ANSIBLE_USER=',
                    'HYPERVISOR_ANSIBLE_HOST=localhost',
                    'HYPERVISOR_ANSIBLE_CONNECTION=local',
                    'HYPERVISOR_ANSIBLE_PASSWORD='
                    ]) {
                        sh "molecule test -s ${scenarioList[i]}"
                    }
                }
            }
        }
    }
}

@NonCPS
List<List<?>> mapToList(Map map) {
  return map.collect { it ->
    [it.key, it.value]
  }
}

parallel nodes