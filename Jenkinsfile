pipeline {
    agent any
    stages {
        stage("Tools initialization") {
            steps {
                sh "mvn --version"
                sh "java -version"
            }
        }
        stage("Checkout Code") {
            steps {
                checkout scm
            }
        }
        stage("Check Code Health") {
            when {
                not {
                    anyOf {
                        branch 'main';
                        branch 'develop'
                    }
                }
           }
           steps {
               sh "mvn clean compile"
            }
        }
        stage("Run Test cases") {
            when {
                branch 'develop';
            }
           steps {
               sh "mvn clean test"
            }
        }
        //stage("Check Code coverage") {
        //    when {
        //        branch 'develop'
        //    }
        //    steps {
        //       jacoco(
        //            execPattern: '**/target/**.exec',
        //            classPattern: '**/target/classes',
        //            sourcePattern: '**/src',
        //            inclusionPattern: 'com/iamvickyav/**',
        //            changeBuildStatus: true,
        //            minimumInstructionCoverage: '30',
        //            maximumInstructionCoverage: '80')
        //   }
        //}
        stage("Build & Deploy Code") {
            when {
                branch 'develop'
            }
            steps {
                sh "mvn clean install"
            }
        }
        
        stage("Artifact checkup") {
           steps {
             sh "ls -ltr /var/lib/jenkins/.m2/repository/com/souvc/springboot/spring-boot-sample-hello/1.0-SNAPSHOT "
           }
        }
    }
 }
