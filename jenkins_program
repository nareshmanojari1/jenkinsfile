
node{


if (env.BRANCH_NAME=='master') {

   Checkout()

   Junit()

   sonarcube()

   buildAndPublishToArtifactory()

  }

}

 def Checkout(){

    stage 'Checkout SCM'

    checkout scm

}

def Junit() {

    stage 'junit test'

  sh 'mvn test'

  }


def sonarcube() {

    stage('SonarQube analysis') {

         

   withSonarQubeEnv('Sonar') {

                

   sh 'mvn sonar:sonar '
           

 }      

}

}

def build(){

   stage 'build'

   sh 'mvn clean compile install -U -Dskiptest=true '

   }
  

   def deploy(){

   stage 'deploy'

   sh ''

}                

def CleanBuild() {

    stage 'Build'

    sh 'mvn clean compile'
           

}

def buildAndPublishToArtifactory() {


    stage ('Distribute binaries to Jfrog Artifactory') {

    def SERVER_ID = '1'

    def server = Artifactory.server SERVER_ID

    def buildInfo = Artifactory.newBuildInfo()

    build
