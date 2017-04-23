pipeline {
  agent any

  stages {
    stage("SCM Update"){
    	steps {
    		sh "git remote add lede git://git.lede-project.org/source.git || true"
    		sh "git fetch lede"
            sh "git branch -D build"
    		sh "git checkout -b build"
    		sh "git merge lede/master"
    		sh "./scripts/feeds update -a"
    		sh "./scripts/feeds install -a"
    }}
    stage("Build Image"){
	    steps {
	        sh "make defconfig"
	        sh "make -j4"
    }}
  }
  post {
      success {
          sh "git remote add githubssh git@github.com:admiral0/lede-rango.git || true"
          sh "git fetch githubssh"
          sh "git push githubssh build:master"
	  sh "rsync -avh --delete bin/* /srv/http/lede/jenkins"
      }
  }
}

