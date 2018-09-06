---
layout: post
title: Integrate Jenkins and Gitlab
---

After integrating Jenkins with Gitlab a few times on my last projects I ran on the same issues hence this article to summarise what I usually do.

First, we need to download the Gitlab plugin on Jenkins if it has not already been done.

For the Ops part that will probably be done only once you should go to your Jenkins.

Navigate to *Manage Jenkins* then *Configure System* and then scroll down to the *Gitlab* section. Check: *enable authentication for /project end-point*. Put a connection name that makes sense for you. Your Gitlab host url is something like:https://YOUR_GITLAB_HOST_NAME.com The credentials should be filled with your Gitlab credentials and if you don't have any you still can create some by clicking the Add button.

Then, navigate to your Jenkins project. Click on *Configure* then *Build Triggers*. You should check *Build when a change is pushed to GitLab* and then check the features you need and generate a Secret Token.

Keep the gitlab web hook URL and the generated token until the gitlab part is not finished.

Finally, go to your Gitlab project and navigate to the Integration's menu.

Fill it with like that:

* URL:  gitlab web hook URL from Jenkins
* Secret Token: jenkins generated token
* Check whatever you want / need in the trigger possibilities
* click “Add Webhook”

And now we just have to test it once it appears in the list of webhooks below and it should make your Jenkins project run.

Hope this helps.
