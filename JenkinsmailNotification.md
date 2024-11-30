# Steps to set up email notification in Jenkins:
## 1.	Create App Password in Google Account:
*	Log in to your Google account.
*	Navigate to the security settings.
*	click on 2 step verification & go at the end
*	Look for the option to create an App Password.
*	Generate a new App Password and note it down. This will be used for SMTP authentication in Jenkins.
## 2.    Configure Email Notification in Jenkins:
*	Log in to your Jenkins dashboard.
*	Go to "Manage Jenkins" from the sidebar.
*	Select "Configure System".
*	Locate the section for "E-mail Notification" or "Extended E-mail Notification".
## 3.	SMTP Configuration:
*	In the SMTP server field, enter smtp.gmail.com.
*	Set the SMTP port to 465.
*	Ensure that SSL is checked to enable secure communication.
## 4.	Credentials:
*	Under the SMTP Authentication section, select "Use SMTP Authentication".
*	Enter your Google email address in the "User Name" field.
*	Use the App Password generated earlier as the "Password".
## 5.	Test Configuration:
*	Scroll down to the bottom of the configuration page.
*	Click on the "Test configuration by sending test e-mail" button.
 
*	Verify that you receive the test email in your inbox.
## 6.	Save Changes:
*	Once the test email is successfully sent and received, click on "Save" to apply the changes.



## 7.	Sample Scipt
post {
    always {
        script {
def jobName = env.JOB_NAME
def buildNumber = env.BUILD_NUMBER
def pipelineStatus = currentBuild.result ?: 'UNKNOWN'
def bannerColor = pipelineStatus.toUpperCase() == 'SUCCESS' ? 'green' :
'red'


def body = """<html>
<body>
<div style="border: 4px solid ${bannerColor}; padding:
 
10px;">



10px;">
 

<h2>${jobName} - Build ${buildNumber}</h2>
<div style="background-color: ${bannerColor}; padding:

<h3 style="color: white;">Pipeline Status:
 
${pipelineStatus.toUpperCase()}</h3>
</div>
 
