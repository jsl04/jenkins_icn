pipeline {
  agent {
    node {
      label 'kubernetes-prp'
    }

  }
  stages {
    stage('Setup prefixes and routes') {
      steps {
        sh 'vppctl hicn punting add prefix c001::/16 intfc <GigabitEthernetb/0/0> $punting_ip'
      }
    }

  }
  environment {
    dataset_name = 'SRR5139397_1.fastq.gz'
    dataset_prefix = ' b001'
    icn_node_1 = ' 10.10.3.20'
    icn_node_2 = '10.10.3.10'
    punting_ip = ''
  }
}