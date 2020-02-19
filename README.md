Perequisites for Simple CI/CD:
1)Github account
2)Simple java or any other language project
3) Jenkins server
4) Maven and git installation and configuration withy jenkins
5) Tomcat or any other server
Steps:
1) We need to create the github account and need admin  access to the github repo that developers are using to checkout there code. Sharing you my github repo i have created and clone the github repo provided by you and made some commits on it.
https://github.com/MohdA/sample_devops
2) Jenkins Installation and configuration:
First, you need to install JDK. Once Java is running, you need to install Jenkins. you can download it from jenkins official site and download the jenkins latest packeage for windows, Ubuntu etc and the run the jenkins exe file.
once installation part get completed yu will automatically be redirected to a local Jenkins page i.e http://localhost:8080 in a browser.
Then  unlock Jenkins, copy the password from the file at C:\Program Files (x86)\Jenkins\secrets\initialAdminPassword and paste it in the Administratorpassword field. Then, click the "Continue" button. You can reset password later from jenkins dashboard.
Then install suggested or selected Plugins. I will prefer to intall slected pluginbs that bwe are going to use in setting up jenkins pipelins CI&CD jobs. 
3) Installing and Configuring Maven  and Git on server.
a) Download Maven on jenkins server from Maven official site using wget command and also setup M2_Home and M2 paths in .bash profile of user.
b) install git also using yum install git -y
then login to Jenkins Console for configuration part and install Maven and Git plugin and restart  the jenkins.
Also set Maven and Git Path from Manage Jenkins Global Tool configuration.
4) Also setup and configure Tomcat server where we want to deploy over war or jar file.
steps  to install tomact on linus:
a) Nee to launch linux server
b) Install java and set path as we already did on our jenkins server
3)Download Tomcat package from tomcat official site and extract giz file to your directory where you want to install it.
d) then we need to add users to tomcat-user.xml file under conf directory in tomcat. these users will use used in future to access in jenkins.
e) start the tomcat server using startup.sh
Now setting up jenkins pipeline for continous deployment whenever code get commit in Github:
1) Jenkins is already setup using above steps and code is already pused to our github repo. Noe let's make a jenkins job for continous deployment.
Login to your jenkins dashboard and click on new itam to create a new project that can be Freestyle project or Maven project. We are using Maven project in our projects.
Now mentioned the project name and then go to source code managment  where you source code is availble. Our code is availble at github so we need to intsall github plugin and provide the repo url and add your credentials . Also mention the branches to build. Bydefault it is master branch. now save it
Now go to Build trigger and there are many options to build your code by checking the github periodically or when github trigger for GITScm pooling or we can also Poll SCM.
Then go to build and provide pom.xml path and goals to create the war or jar file.
Then we need to deploy this war file to our tomcat server and for that need to provide the tomcat credentials in your Jenkins and also need to install deploy pluggin in your jenkins
Once it done go to the post build action and mention the war or jar file path and container you using( which is tomcat in our case) and also provide the tomcat server credentails and save the job.
Now when somebody go and change the job it will automatically the new build on this server and it is being done bt build trigger option we selected and used poll SCM and mentioned cron job type entry for ex ***** it will check our code every minute for any change and trigger the build once there will be any change in code.
----------------------------------------------------------------------------------------------------------------
By doing this we can achieve the CI/CD. There are further more things like using Ansible playbooks for configuration managments. We can deploy the build on docker containers.
We can monitore our tasks and process using Geneos or other monitoring tool and further more things.
I have cloned the sample github job you provided and made some more commits , made another branch and made changes on that branch and than merge it back to the master branch. 
