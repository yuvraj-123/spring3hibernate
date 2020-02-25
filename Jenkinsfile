pipeline {
         agent any
         stages {
                 stage('Git clone') {
                 steps {
                     git "https://github.com/opstree/spring3hibernate"
                     echo 'Hi, this is Yuvraj Singh '
                 }
                 }
                 stage('code stability'){
                 steps {
                    sh 'mvn clean package'
                     echo 'make the jar file '
                 }
                 }
                 stage('code quality'){
                 steps {
                     echo "assured quality, thanks"
                      sh 'mvn findbugs:findbugs && mvn checkstyle:checkstyle'
                 }
                 }
                 stage('Code Coverage'){
                 steps {  
                     echo "thnaks"
                     sh 'mvn cobertura:cobertura' 
                }
                }
                 stage ('email notify'){
                    steps {
                        echo "sending mail to receipent "
                        emailext (
                         subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
                         body: """<p>Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME}</a></p>""",
                         to: "kumar040997@gmail.com",
                         from: "yuvrajsinghsolank03@gmail.com"
)
                    }
                }
                stage ('slack notify'){
                    steps {
                        echo "send the slack notification"
                       slackSend channel: 'chuspa-rg', message: 'new msg go1111111111111111111111111111', tokenCredentialId: 'slack-yuvi'
                    }
                }
                stage ('publish code coverage'){
                    steps {
                        echo "publish code coverage "
                        cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                    }
                }
                stage ('checkstyle report'){
                    steps {
                        echo "publish checkstyle report"
                        checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/checkstyle-result.xml ', unHealthy: ''                    }
                }
            }
         }
