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

    stage('setup forwarder') {
      steps {
        sh 'add connection UDP michNode <mich ip> 33567 <NW IP> 33567'
        sh 'add route mich_node c001 0'
      }
    }

    stage('run Higet') {
      steps {
        sh 'higet -O - http://hicn-http-proxy/SRR5139397_1.fastq.gz -P b001'
      }
    }

  }
}