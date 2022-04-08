node
{
    def mavenHome = tool name: "maven_3.6.3"
    def JAVA_HOME = tool name: "jdk8.1"   
    env.JAVA_HOME = "${JAVA_HOME}" 

stage ('checkoutcode')
{
git branch: 'development', credentialsId: '1b69de72-6dc0-4394-ba46-6b37ed3a1abb', url: 'https://github.com/bossrachita/maven-web-application.git'
    }
stage ('build')
 {
          sh "${mavenHome}/bin/mvn clean package"
 }

stage ('checkcodequality')
 {
     sh "${mavenHome}/bin/mvn sonar:sonar"
        }

stage ('store to build artifact')
   {
sh "${mavenHome}/bin/mvn deploy"
         }
stage ('deploy')
{
    sshagent(['f732640b-9205-4de6-94cc-bd0f68a30935']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.110.210.242:/opt/apache-tomcat-9.0.60/webapps/"
}
}
}
