pipeline {
   agent any
  
  stages {
    stage(' GIT CHECKOUT'){
      steps{
        git branch: 'main', url:'https://github.com/ShashBott/javacicode.git'
           }
          }
     stage ('UNIT TESTING') {
      steps {
        sh 'mvn test' 
            }
                             }
}
}
