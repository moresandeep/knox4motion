# knox4motion

This repo provides some basic Knox configuration for motion (http://www.lavrsen.dk/foswiki/bin/view/Motion/). I am using this setup on my Raspberry Pi. 
Few points to note:
* Motion and Knox re running on the same host (hence the 'localhost' reference in the sandbox.xml for motion service)
** If you are running motion on a different machine (ideal) update the following section in the config/sandbox.xml
   ```
   <service>
       <role>MOTION</role>
       <url>http://my_hostname_or_ip:8081</url>
   </service>
   ``` 
** Knox in this case uses linux PAM authenication as a result the Motion interface is secured by Basic authentication, so you can authenticate using the users configured on your machine i.e. if you are using Raspberry Pi you can login with user:password - pi:raspberry (if you did not change the default settings, in which case PLEASE change the password).
** Some housekeeping for PAM to work on Raspberry Pi (Raspbian) - you might not need if you are using Centos or RHEL
*** cd /lib/arm-linux-gnueabihf
*** sudo ln -s libpam.so.0.83.1 libpam.so
*** In Knox gateway.sh script (knox-0.12.0/bin/gateway.sh) if you are using version less than Knox 0.12 then you might have to do some more updates.
**** APP_JAVA_LIB_PATH="-Djava.library.path=/lib/arm-linux-gnueabihf/“
*** Add the user you will be running Knox under to shadow group (I know it's bad but for now this works)
**** sudo usermod -a -G shadow <knox-user>



