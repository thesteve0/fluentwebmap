#The code to accompany Fluent Webinar 2014

This code actually belongs to a [blog piece](https://openshift.redhat.com/community/blogs/using-nodejs-mongodb-express-for-your-spatial-web-service-and-its-free) written on OpenShift.com 

========

Running on OpenShift
----------------------------

Create an account at http://openshift.redhat.com/

Create a Node.js application and add a MongoDB cartridge to the app

    rhc app create fluentwebmap nodejs-0.1 mongodb-2.2 -s -g medium
    
You can name your application anything you want - it does not have to be fluentwebmap.

The command line above also uses -s to make it a scalable application, where MongoDB and Node.JS are on different gears and therefore do not have to share resources. It also allows them to scale independently

Since I am a paid user, I am also choosing to use medium gears (1 gig of memory) for my applications.


now add this upstream node repo


    cd fluentwebmap
    git remote add upstream -m master https://??????
    git pull -s recursive -X theirs upstream master
    
Then push the repo upstream

    git push
    

Now, ssh into the application.

Once the data is imported you can now checkout your application at:

    http://fluentwebapp-$yournamespace.rhcloud.com/


License
-------

This code is dedicated to the public domain to the maximum extent
permitted by applicable law, pursuant to CC0
http://creativecommons.org/publicdomain/zero/1.0/
