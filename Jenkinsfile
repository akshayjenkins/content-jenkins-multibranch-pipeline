pipeline {
  agent any

  stages {
    stage('build') {
      steps {
        sh 'javac -d . src/*.java'
        sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
        sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
      }
    post {
    success {
      archiveArtifacts artifacts: 'rectangle.jar', fingerprint: true
    }
  }

    }
    stage('run') {
      steps {
        sh 'java -jar rectangle.jar 7 9'
      }
    }
stage ('promote Dev to Master') {
when {
   branch 'development'
}

steps {
echo 'stashing Local changes'
sh 'git stash'
echo 'checkout Dev'
sh 'git checkout development'
sh 'git pull origin'
echo 'git checkout master'
sh 'git checkout master'
echo 'Merging with Master'
sh 'git merge development'
echo 'psuh origin to master'
sh 'git psuh origin master'
}
} 
 }
 }
