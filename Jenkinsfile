node('master')
{

def mavenhome=tool name: "maven3.6.3"
stage('CheckoutCode') {
    git branch: 'development', credentialsId: 'Github', url: 'https://github.com/naren-technologies/maven-web-application.git'
}

stage('Building Code') {
    sh "${mavenhome}/bin/mvn clean package"
}

stage('Execute sonarqube report ') {
    sh "${mavenhome}/bin/mvn sonar:sonar"
}
    
stage('Pushing builds to Aertifact')   {
    sh "${mavenhome}/bin/mvn deploy"
} 

stage('Deploy build into tomcat server') {
    deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://192.168.100.200:9999/')], contextPath: 'Narendra', war: '**/maven-web-application.war'
}
    
  
}
