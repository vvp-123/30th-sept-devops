#!/usr/bin/env groovy

import java.net.URL

node{
    stage('Git Checkout'){
        git 'https://github.com/npsoni88/DevOpsClassCodes.git'
    }
    stage('Compile'){
        withMaven(maven:'MyMaven'){
            sh 'mvn compile'
        }
    }
    stage('Test'){
        try{
            withMaven(maven:'MyMaven'){
                sh 'mvn test'
            }
        } finally{
            junit 'target/surefire-reports/*.xml'
        } 
    }
    stage('Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
   
}
