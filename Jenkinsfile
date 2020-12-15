node{
    def mavenHome= tool name: "maven", type: "maven"
    stage('Git Clone'){
        git url: 'https://github.com/kagithanaveen/simple-java-maven-app.git'
    }
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('Build Docker Image'){
        sh "docker build -t naveen1997/simple-java-maven-app ."
    }
    stage ('Docker Login and Push'){
        withCredentials([string(credentialsId: 'Docker1', variable: 'Docker1')]) {
        sh "docker login -u naveen1997 -p ${Docker1}"
    }

    
        sh "docker push naveen1997/simple-java-maven-app:latest"
    }
    
    stage('Deploy as Container in Deployment Server'){
       sshagent(['Docker']) {
      
        sh "docker login -u naveen1997 -p Naveen@1997"
        
        sh "ssh -o StrictHostKeyChecking=no ubuntu@13.250.3.217 docker rm -f webappcontainer || true"
        
        sh "ssh -o StrictHostKeyChecking=no ubuntu@13.250.3.217 docker run -d -p 8080:8080 --name webappcontainer naveen1997/simple-java-maven-app:latest"
            
            
        }

    }
}
