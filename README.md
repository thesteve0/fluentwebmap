#The code to accompany [Fluent Webcast](http://www.oreillynet.com/pub/e/3017) 2014

This code actually belongs to a [blog piece](https://openshift.redhat.com/community/blogs/using-nodejs-mongodb-express-for-your-spatial-web-service-and-its-free) written on OpenShift.com 


A very simple application that lets us serve up points on an OpenStreetMap base layer. 
If you want to use your own data you can replace the contents of parkcoord.json with your 
own data and import that instead.


Running on OpenShift
--------------------

Create an account at http://openshift.redhat.com/

Create a Node.js application and add a MongoDB cartridge to the app

    rhc app create fluentwebmap nodejs-0.1 mongodb-2.2 -s -g medium
    
You can name your application anything you want - it does not have to be fluentwebmap.

The command line above also uses -s to make it a scalable application, where MongoDB 
and Node.js are on different gears and therefore do not have to share resources. It also 
allows them to scale independently.

Since I am a paid user, I am also choosing to use medium gears (1 gig of memory) by using 
the -g flag for my applications.


Now add this upstream node repo

    cd fluentwebmap
    git remote add upstream -m master https://github.com/thesteve0/fluentwebmap.git
    git pull -s recursive -X theirs upstream master
    
Then push the repo upstream

    git push
    
You can now check out your application at:

    http://fluentwebmap-$yournamespace.rhcloud.com/


Tuning for your application
---------------------------

The title of the webpage ("map of parks") can be changed in public/index.html.
The heading title ("National Park Locator") can be changed in public/index.html.
The initial location at the center of the map can be changed by modifying the setView()
call in public/index.html.


Creating the MongoDB database
-----------------------------
To create the webmap database with the parkpoints collection, run the following command:

    mongoimport -d webmap -c parkpoints < parkcoord.json


License
-------

This code is dedicated to the public domain to the maximum extent
permitted by applicable law, pursuant to CC0
http://creativecommons.org/publicdomain/zero/1.0/
