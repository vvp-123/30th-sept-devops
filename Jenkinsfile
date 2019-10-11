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
    stage('Code Review'){
        try{
            withMaven(maven:'MyMaven'){
                sh 'mvn pmd:pmd'
            }
        }finally{
            pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
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
    stage('Code Coverage'){
        try{
            withMaven(maven:'MyMaven'){
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
        }finally{
            cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
        }
    }
    stage('Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
   
}
