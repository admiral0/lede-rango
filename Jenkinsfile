pipeline {
  agent any

  stages {
    stage("Feeds Update"){
    	steps {
    		sh "./scripts/feeds update -a"
    		sh "./scripts/feeds install -a"
    }}
    stage("Build Image"){
	    steps {
	        sh "cp my_config .config"
	        sh "yes '' 2>/dev/null | make oldconfig"
	        sh "make -j4"
    }}
  }
  post {
      success {
	  sh "rsync -avh --delete bin/* /srv/http/lede/jenkins"
      }
  }
}

