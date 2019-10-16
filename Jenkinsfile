#!/usr/bin/env groovy

//Pipeline as Code example
import java.net.URL
import hudson.model.*

node {
    stage('Git Checkout'){
        git 'https://github.com/rakeshdhull/DevOpsClassCodes.git'
    }
    stage('Compile'){
        withMaven(maven:'DevopsMaven'){
            sh 'mvn compile'
        }
       
    }
    
    stage('Test'){
        withMaven(maven:'DevopsMaven'){
            sh 'mvn test'
        }
    }
    
    stage('CoverageCheck'){
        echo 'Coverage Check'
        withMaven(maven:'DevopsMaven'){
            sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
        }
        cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
        
    }
    
    stage('Package'){
        withMaven(maven:'DevopsMaven'){
            sh 'mvn package'
        }
    }
    
}
