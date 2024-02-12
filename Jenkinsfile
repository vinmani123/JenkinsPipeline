node{

   def tomcatWeb = '/home/osboxes/Downloads/apache-tomcat-9.0.80/webapps'
   def tomcatBin = '/home/osboxes/Downloads/apache-tomcat-9.0.80/bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/vinmani123/JenkinsPipeline.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'Maven', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.sh"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     sh "copy target\\JenkinsPipeline.war \"${tomcatWeb}\\JenkinsPipeline.war\""
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         sh "${tomcatBin}\\startup.sh"
         sleep(time:100,unit:"SECONDS")
   }
}
