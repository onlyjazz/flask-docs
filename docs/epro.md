<a href="https://www.flaskdata.io">![Screenshot](img/flaskdata_logo.PNG)</a>
#ePRO
This is patient's diary.


##What is Flask PRO?
* Flask PRO is an online ePRO app
* Forms PRO unlimited subjects, forms and data. 
* You can create the ePRO yourself using a super friendly interface.  
* Runs on desktops, notebooks, tablets and phones.

##Prerequisites
###Study definition
To define [study](./manage_studies.md#add-study) with ePRO, the study should be defined as the following:
1. **Enable patient reported outcome module?**
3. **PRO URL**: should be **https://epro.flaskdata.io**, (If study has another PRO then FlaskData fill the *PRO URL* field with your study's PRO URL).

![Screenshot](img/epro/epro_study_definition.PNG)

###Forms definitions
To define ePRO questionnaire, you need to create [CRF/s](./manage_forms.md#crfs) and [Event](./manage_forms.md#event-definitions) includes your diary CRF/s first.

Second you need to create [Study Schedule](./manage_forms.md#study-schedules) with your period diary.

![Screenshot](img/epro/epro_study_schedule.PNG)

##Welcome Email and SMS
When subject has been created the patient gets a welcome email and SMS with PRO link.

He/She is invited entering and fill his/her diary.

If patient forgets his password [site role user](./manage_users.md#profile) (like CRC or PI) can go to [subject's profile](./manage_subjects.md#actions) page and send him Welcome back/Reset password email.

![Screenshot](img/epro/subject_actions.PNG)

##Subject invited
When patient gets a welcome emil/SMS he/she should click on the link.

The patient is invited to choose a password.


Then he logins to his PRO.

##








