
import jenkins.model.*

node {
	def HOST = "10.86.87.68"
	def CREDENTIAL = "IDS"
	def PACKAGE = '''$TEST_GIT_ABAP'''
	def COVERAGE = 80
	
    stage('Preparation') {
        deleteDir()
        git poll: true, branch: 'master', url:'https://github.com/pacroy/abap-rest-api.git'
		dir('sap-pipeline') {
			bat "git clone https://github.com/pacroy/abap-ci-postman.git ."
		}
    }
    
	def sap_pipeline = load "sap-pipeline/sap.groovy"
	sap_pipeline.abap_unit_coverage(HOST,CREDENTIAL,PACKAGE,COVERAGE)
	sap_pipeline.abap_sci(HOST,CREDENTIAL,PACKAGE)
	sap_pipeline.sap_api_test(HOST,CREDENTIAL)
}
/*
import jenkins.model.*

node {
	def skip_pipeline = false
    stage('Preparation') {
        deleteDir()
        git poll: true, branch: 'master', url:'https://github.com/phucdt4/abapgittest.git'
		dir('sap-pipeline') {
			bat "git clone https://github.com/pacroy/abap-ci-postman.git ."
		}
    }
    
    stage('ABAP Unit and Code Coverage') {
		dir('sap-pipeline') {
			withCredentials([usernamePassword(credentialsId: 'IDS', usernameVariable: 'abapleader', passwordVariable: 'TH1234567a@')]) {
				bat "newman run abap_unit_coverage.postman_collection.json --insecure --bail --environment NPL.postman_environment.json --global-var username=$USERNAME --global-var password=$PASSWORD --timeout-request 120000"
			}
		}
    }
    
    stage('ABAP Code Inspector') {
		dir('sap-pipeline') {
			withCredentials([usernamePassword(credentialsId: 'IDS', usernameVariable: 'abapleader', passwordVariable: 'TH1234567a@')]) {
				bat "newman run abap_sci.postman_collection.json --insecure --bail --environment NPL.postman_environment.json --global-var username=$USERNAME --global-var password=$PASSWORD --timeout-request 120000"
			}
		}
    }
    
    stage('SAP API Tests') {
			withCredentials([usernamePassword(credentialsId: 'IDS', usernameVariable: 'abapleader', passwordVariable: 'TH1234567a@')]) {
				try {
					bat "newman run SimpleRESTTest.postman_collection.json --insecure --bail --environment NPL.postman_environment.json --reporters junit --global-var username=$USERNAME --global-var password=$PASSWORD --timeout-request 10000"
				} catch(e) {
					skip_pipeline = true
					currentBuild.result = 'FAILURE'
				}
				junit 'newman/*.xml'
			}
    }
}
*/
