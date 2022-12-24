# CI-CD-Project-1

--------------------------------------------------------------------------------------------------------------------
      IN THIS PROJECT WE TRIED TO EXECUTE 3 JOBS (2 PIPELINE, 1 FREE STYLE) ON MASTER SERVER WITH JENKINS
---------------------------------------------------------------------------------------------------------------------

<--- IN PIPELINE 1 JOB --->

Here we took one slave server, We used slave as the node in pipeline and implement everything from master to implement 3 stages as follows:

  For this we need the jenkins plugin(DEPLOY OVER CONTAINER)
  
  Stage-1 is taking a git repo to fetch src code containing pom.xml file file 
  
  Stage-2 has 2 steps,1st is to build the file from the git repo and 2nd is renaming the war file from build for naming convention to use
  
  Stage-3 is to deploy on tomcat, here we copy the war file to the tomcat’s workspace
  
  WE CAN INTEGRATE WEBHOOKS TO THE PIPELINE
 
<--- IN PIPELINE-2 JOB --->

This is pipeline is just a small addon to the pipeline -1 job

  Here we try to implement everything on master and try deploying on slave 
  
  For this we need the jenkins plugin(SSH AGENT)
  
  On the deploying stage, we used scp command to copy war file from master server to slave’s tomcat server webapps folder
  
  One small twerk we did  inorder to avoid permission denied error from the scp command is, adding user using chown command to the apache.tomcat folder on  slave (user from which we’re trying access the folder on scp command)
  
  WE CAN INTEGRATE WEBHOOKS TO THE PIPELINE
  
<--- IN FREESTYLE JOB --->

This job is to execute playbook on slave server to setup tomcat server from master

  For this we need the jenkins plugin(PUBLISH OVER SSH)
  
  After installing the plugin, we configure system on jenkins to add a SSH server
  
  Now on configuring this job, we use post build steps(send build artifacts over ssh) to excute the ansible playbook on slave
  
WE CAN CI/CD LAST TWO JOBS BY ADDING build after pipeline job ON FREESTYLE JOB BUILD TRIGGER CONFIG SO THAT, SO WHEN THERE IS CHANGE IN SRC CODE ON GITHUB PIPELINE TRIGGERS BECAUSE OF THE WEBHOOKS WHICH THEN TRIGGERS THIS FREESTYLE JOB.
