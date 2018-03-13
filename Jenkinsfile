pipeline {
    agent {
        label 'master'
   }
          stages {
              stage ('Unit Tests'){
                  steps{
                     sh 'ant -f test.xml -v'
                     junit 'reports/result.xml'
              }
          }
          stage ('build'){
              steps{
                  sh 'ant -f build.xml -v'
              }
          }
          stage ('deploy'){
              steps {
                  sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
              }
          }
          stage ("Running on CentOS"){
                              agent {
                          label 'CentOS'
                                 }
                                 steps{
                                     sh "wget http://192.168.1.89/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
    								sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4 "
                                 }
                              }
	}
post {
    always {
          archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
	}
   }
}
