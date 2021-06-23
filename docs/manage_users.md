<a href="https://www.flaskdata.io">![Screenshot](img/flaskdata_logo.PNG)</a>
#Manage Users
In the left menu bar click on Users.

On this page, you can add Users to your study, edit Users, assign Users to Sites, etc.

You can filter Users by study, site, or by using the **Search** filter and clicking **APPLY**

![Screenshot](img/user/users_index_filter.PNG)

##Default Users
By default, you have 4 Users assigned to your study:

    1.Customer admin User - This is your User!
    2.CRC Default - CRC User
    3.PI Default - PI User
    4.CRA Default - CRA User
![Screenshot](img/user/default_users.PNG)

**Each default User has another permissions.**

##Edit User
Edit the default Users to your specific Users one by one, by clicking the **ACTIONS**-> **EDIT** option. 

![Screenshot](img/user/users_index_actions.PNG)

###Profile
In the User profile page there is a pencil icon in the right corner of **Profile card**, click on it in order to edit the User properties.

![Screenshot](img/user/user_edit.PNG)

After you create a new User or modify their email, you can send them an email to create a password by clicking on **Send create password**. 

This step does not need to be taken - your Users can log in with their Google account.

!!! note "User properties"

    In edit the User Profile action, you can change a some User parameters
    
    1. *Role*: there are 3 roles
        * Customer Admin - User has all customer permissions - add/edit studies, users, sites, alerts, etc.
        * Study Role - User has study permissions - to see all study data (from all of the sites)
        * Site Role - User has site level permissions - to see his site data, add subject to his site, create events and CRFs for the subject.  
    2. *Form designer*: define if the User has Forms permissions - add/edit/delete Events and CRFs from the system (by default only customer admin Users can do it).
    3. *Subscribe to Alerts*: defines if the User will get alerts from this study (according to the alert rules).

###Studies
In the **Studies card** you can see the User's studies

![Screenshot](img/user/user_profile_studies_card.PNG)

###Sites
In the **Sites card** you can see the User's sites (if the User is study role or customer admin he can see all study sites)

![Screenshot](img/user/user_profile_sites_card.PNG)

###Comments
In the **Comments card** you can add comments about this User.
Write your comments and click on the **ADD COMMENT** button

![Screenshot](img/user/user_profile_comments.PNG)

##Mange User sites
In User profile page you have an option to manage User sites.

![Screenshot](img/user/user_profile_actions_button.PNG)

!!! note
 
    You only have this option if the User is a Site Role User, otherwise the User has permissions to all study's sites.

In manage User sites page you can add/remove sites from User privileges.

![Screenshot](img/user/user_manage_user_sites.PNG)

##User actions
In User profile page you have **ACTIONS** green button.
In these actions button you have a few actions options:

1. **Send create password** - By clicking on this option you email the User with create a new password request.
2. **Login as this User** - By clicking on this option you login to the system like you are this User.
3. **Modify password** - By clicking on this option you can modify the User password.

    ![Screenshot](img/user/user_profile_modify_pass.PNG)

##Add User
To add a User click on the **ADD USER** green button in Users index page.

![Screenshot](img/user/users_index_add_user.PNG)

The User will be added to the selected study that appears in the title.

![Screenshot](img/study/study_in_title.PNG)

!!! note "User properties"

    1. **Email** should be unique for each User.
    2. [**Role**](./index.md#roles--who-can-do-what) There are 3 optional roles:

         2.1. Customer Admin (2):  Administrator of the customer - has all permissions of this account, create User, create site, build CRFs, etc.
         
         2.2. Study role (3): Has all study permissions - view, extract, etc. to all study data
         
         2.3. Site role (4): Has specific site/s permissions - add subject to his site, fill CRFs, see site's data, etc.

    3. **EDC Role**: more specific role from Role (number 2), it's more relevant for customers that have EDC db.

      | EDC Role ID | Flask Role ID|    EDC Role Name  |        
      |-------------|---------|------------------------|
      |1            |       2 | System Administrator   |
      |2            |       3 | Study Administrator    | 
      |3            |       3 | Study Director         |
      |6            |       3 | Study Monitor          |
      |7            |       3 | Study Coder            |
      |5            |       4 | Site coordinator       |
      |4            |       4 | Principal investigator |
      |8            |       5 | Subject                |
      |9            |       2 | API role               |
      |77           |      2 | RiskGraph role        |

Click on the **SAVE** green button.

![Screenshot](img/user/user_create_new_user.PNG)

The User will get a Welcome message in their email.

![Screenshot](img/user/user_create_success.PNG)
