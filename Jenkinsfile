pipeline {
     agent { docker { image 'python:3.7.2' } }
     environment {
        AWS_DEFAULT_REGION = 'us-east-1'
     }
     stages {
         stage('build') {
             steps {
                    withEnv(["HOME=${env.WORKSPACE}"]) {
                         sh 'pip install flask --user'
                         sh 'pip install boto3 --user'
                         sh 'pip install requests --user'

                     }
                 }
         }
         stage('test') {
             steps {
                 withEnv(["HOME=${env.WORKSPACE}"]) {
                    sh 'python3 test.py'
                 }
             }
         }
         stage('slack notify'){
             steps{
                 slackSend channel: '﻿jenkinsnotify', color: '#1eff00', message: 'The blog services test has passed! '
     }
     }
        stage('Push out to Approved Repo'){
             steps{
                 sh '''#!/bin/bash
                 git config --global user.email "dev.rahman96@gmail.com"
                 git config --global user.name "Mo"
                 git checkout "QA"
                 git add *
                 git commit -m "Jenkins Approved"
                 git push'''
                 
     }
     }
       }
     }