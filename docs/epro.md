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

Patient will get a welcome email again.

![Screenshot](img/epro/welcome_back.PNG)

##Subject invited
When patient gets a welcome emil/SMS
 
 ![Screenshot](img/epro/inbox_email_invite.PNG)
 
 He/she should click on the link.

![Screenshot](img/epro/subject_invite.PNG)

The patient is invited to login with his Google account OR to choose a password.

![Screenshot](img/epro/login_google_account.PNG)

!!!note

    To create a password or reset password - CRC user should reset subject's password by clicking on [Reset password](./manage_subjects.md#subject-profile) option.
    
    The patient will get a reset password email
    
    ![Screenshot](img/epro/reset_pass.PNG)
    
    After Subject set his/her password, He can login to ePRO by Google account or with FlaskData password
    
    ![Screenshot](img/epro/login.PNG) 
    
##Android application

###Installation
If patient has an Android phone, he can install Flask ePRO application from Google play store.

![Screenshot](img/epro/google_play.PNG)

Search flask epro and install it

![Screenshot](img/epro/flask_epro_application.PNG)

After patient install Flask ePRO application he will see the Flask ePRO icon

![Screenshot](img/epro/flask_epro_app_flag.PNG)

Just click on the application and login to ePRO, Enjoy :smile:

###Login to Flask ePRO
Open Flask ePRO application and login to your diary. (To login by email and password you should create the password first by [reset password](./epro_mobile.md#first-login-with-email-and-password) option)

![Screenshot](img/epro/app_login.PNG)

###Enter diary

While patient logins to ePRO, he see his diary for the current date.

He should fill his diary and save.

If there are a few Forms in the diary the next form will be opened when he clicks **SAVE AND NEXT** button.

![Screenshot](img/epro/app_enter_diary.PNG)

!!!important
    
    * If patient filed a part of his diary he can continue later.
    * If patient forgot to fill his diary, He can fill it next 2 days (By [logs](./#logs) option)
 
Required fields are marked with a red asterisk.

If patient try to save the diary with missing information, an error flag appears

Clicking on the error flag opens the error message.

![Screenshot](img/epro/app_error_message.PNG)
 
###Input Data
Patient can click **Input Data** option and fill his diary for the current date.

If he saved his data before, He just see his data and cannot change it.

![Screenshot](img/epro/app_see_diary.PNG)
   
###Logs
Patient can see / continue his diaries in **Logs** option

![Screenshot](img/epro/app_logs.PNG)

###My Account
Patient can change his account definition by clicking on **My Account** option

![Screenshot](img/epro/app_my_account.PNG)

He can change his default language.

![Screenshot](img/epro/app_languages.PNG)

!!!note "Support languages"

    For ePRO lunguages support customer admin user should define it in the [CRFs definition](./manage_forms.md#crfs)
    
    ![Screenshot](img/epro/app_hebrew_forms.PNG)
    
Patient can change ePRO display mode by clicking on theme option.

![Screenshot](img/epro/app_theme_option.PNG)
    
![Screenshot](img/epro/app_theme.PNG)

If he sets the mode as **Dark** he will see something like this:

![Screenshot](img/epro/app_dark_mode.PNG)

###Study information

The patient can see details of the study he is participating in by clicking on the exclamation mark

![Screenshot](img/epro/study_information_icon.PNG)

![Screenshot](img/epro/study_info.PNG)

##FlaskData application
If subject cannot use [Flask ePRO](#android-application) android application he/she can use FlaskData application to enter his/her diary.

It's less beautiful but works great. :+1:

In any case in such a case that the phone does not support Android it is better for the patient to use his desktop.

###Login
Patient should login to FlaskData ePRO URL (https://epro.flaskdata.io)

![Screenshot](img/epro/flask_data_login.PNG) 

###Input Data

When patient login to his diary a diary for the current date opens.

He can start to fill the diary.

![Screenshot](img/epro/flaskdata_enter_data.PNG)

If there are another Forms in the diary he should click **SAVE AND NEXT** button

![Screenshot](img/epro/flaskdata_save_and_next.PNG)

If he filled the last form he should click **FINISH** button

![Screenshot](img/epro/flaskdata_finish_button.PNG)

When patient finish fill diary a success message appears

![Screenshot](img/epro/flaskdata_success.PNG)

To go back to **Input Data** click on the icon

![Screenshot](img/epro/flaskdata_inputdata_icon.PNG)

###Logs

Patient can see his diaries by **Logs** option

![Screenshot](img/epro/flaskdata_logs_option.PNG)
 
![Screenshot](img/epro/flaskdata_logs.PNG)
 
By logs option patient cannot change his diaries, just see them
 
![Screenshot](img/epro/flaskdata_view_mode.PNG)

!!!note "Forget Option"

    1. If patient filled diary but didn't finish all his diary forms he can continue from Logs option
    
        He can continue filling data for yesterday's diary and for the diary of two days ago.
    
    2. If patient forgot to fill his diary he can enter data for yesterday's diary and for the diary of two days ago.
   
###My Account

To see account definition click on **My Account** icon

![Screenshot](img/epro/flaskdata_my_account.PNG)

!!!note Change language

    Patient can change the language by click on Languages icon - this option change the language for this login but it doesn't change patient account definitions, So in the next login the language will be the default language again.    
    ![Screenshot](img/epro/langauges_icon.PNG)

Save patient's account information after changing.

![Screenshot](img/epro/flaskdata_update_my_account.PNG)

###Study information
The patient can see details of the study he is participating in by clicking on the exclamation mark

![Screenshot](img/epro/flaskdata_study_info.PNG)

![Screenshot](img/epro/flaskdata_study_information.PNG)

###Logout
After patient finish filling his diary he can logout from the system by clicking **Logout** icon.

    
    





    







