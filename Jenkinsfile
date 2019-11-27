#!/usr/bin/env groovy
pipeline{
        agent any
          triggers {
  pollSCM 'H/2 * * * *'
          }
 stages{
     stage('Git checkout'){
     //invoking Git repository
     step{
    git 'https://github.com/balucc/Addressbook.git'
     }}
 }
