pipeline {
  agent {
    docker {
      image 'python:alpine3.7'
      args '-p 5000:5000'
    }

  }
  stages {
    stage('Deploying ICN Container') {
      steps {
        sh 'docker pull icnteam/vhttpproxy:amd64'
        sh '''docker run --cap-add=NET_ADMIN              \\
           --device=/dev/vhost-net          \\
           --device=/dev/net/tun            \\
           -p 33567:33567/udp               \\
           -e HICN_LISTENER_PORT=33567      \\
           -e ORIGIN_ADDRESS=www.google.com \\
           -e ORIGIN_PORT=80                \\
           -e CACHE_SIZE=10000              \\
           -e HICN_MTU=1200                 \\
           -e FIRST_IPV6_WORD=c001          \\
           -e HICN_PREFIX=http://httpserver \\
           -e DEFAULT_CONTENT_LIFETIME=7200 \\
           -e USE_MANIFEST=true             \\
           -e UDP_TUNNEL_ENDPOINTS=remote_ip1:remote_port1,remote_ip2:remote_port2 \\
           -d --name vhttpproxy icnteam/vhttpproxy'''
      }
    }

  }
}