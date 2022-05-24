pipeline{
agent {label 'dev'}
triggers {
        pollSCM '* * * * *'
}
stages{
stage('scm'){
steps{
git branch: 'feat01', credentialsId: '6a28a4b2-13ec-41a9-ac29-d9c5bc4228ef', url: 'https://github.com/radhagi/mavenrepo.git'
}
}
stage('build'){
steps{
sh 'mvn package'
}
}
stage('sonar'){
steps{
withSonarQubeEnv('mysonar') {
   sh 'mvn sonar:sonar'
}
}
}
stage('nexus'){
steps{
sh 'mvn deploy'
}
}
stage('tomcat'){
steps{
sh 'scp studentapp-2.1.1-FEAT01-SNAPSHOT.war 54.221.114.177:/var/lib/tomcat/webapps'
}
}

}
}
