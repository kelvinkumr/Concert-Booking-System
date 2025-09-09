## System description
A booking service is required for a small venue, with a capacity of 120 seats. The venue's seats are classified into three price bands, Silver, Gold and Platinum. A concert may run on multiple dates, and each concert has at least one performer. Additionally, a performer may feature in multiple concerts.

The service is to allow clients to retrieve information about concerts and performers, to make and enquire about seats and reservations, and to authenticate users.

When making a reservation, clients may enquire about available seats. They should be informed of any unbooked seats, along with their pricing. Clients may select any number of seats to book. When making a reservation request, double-bookings are not permitted. Only one client should be allowed to book a given seat for a given concert on a given date. Clients may not make partial bookings - either all of a client's selected seats are booked, or none of them are.

Clients may view concert and performer information, and enquire about available seating, whether or not they are authenticated. When authenticated, clients gain the ability to make reservations, and to view their own reservations. Clients should never be able to view the reservation information for other guests.

In addition, clients should be able to subscribe to information regarding concert bookings. Specifically, they should be able to subscribe to "watch" one or more concerts / dates, and be notified when those concerts / dates are about to sell out.

A particular quality attribute that the service must satisfy is scalability. It is expected that the service will experience high load when concert tickets go on sale.

## Running The System
The only way to run the complete system is to package both the client and service projects into WAR files, and deploy them to a running servlet container such as Tomcat.

Fortunately, running Maven's package goal on the parent project will build both WARs as required. However, we will still need to set up a Tomcat (or similar) instance to run the application.

Whichever IDE you use, the first step will be to download a Tomcat installation, if you don't already have one. You can find them here. Get version 8.5.x as an archive (the installer isn't required), download and unzip it somewhere on your machine, and then follow the steps below according to your IDE.

From IntelliJ
Note: This ONLY works in IntelliJ Ultimate edition. Community edition does not support this. Having said that, Ultimate edition is available for free for educational use. Simply sign up for a new account using your University email address.

Within your project, open the Run Configurations dialog (usually available in the top-right corner, or open the search box by tapping double-shift, then type "run configurations"). Either way, pick Edit Configurations. Click on the + button on the top-left of the dialog, then choose Tomcat server → Local.

Name the configuration whatever you like. For the HTTP Port, pick one which is available on your machine, such as 10000.

For the application server, pick one from the list. If none are available, click configure. You'll be able to add one (by browsing to the location where you downloaded Tomcat earlier).

Under the Deployment tab, select both WAR artifacts (client and service) for deployment - these would have been created by IntelliJ's Maven integration (you shouldn't select the exploded versions, but it probably doesn't matter). For the application context, set the service WAR's context to /webservice, and the client WAR's context to /concert-webapp.

Go back to the Server tab. Edit the URL to be http://localhost:10000/concert-webapp/ (altering the port as necessary). Then, click OK.

In the client project, open src/main/java/.../Config.java, and edit the WEB_SERVICE_URI field as appropriate (assuming port 10000, and the contexts identified in step 5 above, you won't need to change this).

In the client project, open src/main/webapp/js/fetch-api.js and edit WEB_URI as appropriate (assuming the contexts identified in step 5 above, you won't need to change this).

From the run configurations dropdown, slect your new configuration and click the play button. The webapp and web service should start, and the browser should eventually open at the URL identified in step 6 above. If it doesn't, you can browse there manually.

When you're done, hit the stop button. Sometimes you may need to click it twice (do so until the stop button is greyed out, and you see a Disconnected from server message in the server output).



From Eclipse
Note: This only works with Eclipse for Java EE Developers, with Tomcat support enabled. If you don't see any of the options mentioned here, it's likely that you don't have these options. You can get them through the Help → Install new software menu, searching for Java EE and Tomcat, respectively.

Open Window → Preferences, then choose Server → Runtime Environments. Click Add, then choose the Apache Tomcat version matching the one you downloaded (which should be v8.5 if you're following along).

Click Next, then browse to where you unzipped Tomcat. Click Select folder, then Apply and Close.

Next, open the run configurations menu (the small dropdown arrow next to the green Play button). Locate Apache Tomcat, and double-click to create a new run configuration.

Go to the Servers View. if it's not on-screen, open it with Window → Show view. Create a new Tomcat server of matching version, and click Finish.

Right-click the newly created server, and choose Open. here, you can configure the HTTP/1.1 port on the right (say, to 10000). Save the config (Ctrl+s).

In the above menu, you can also see / change the Server path and Deploy path. the default is something like .metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps - which you can use, or you can change it to anywhere on your machine. Again, save the config.

Run maven's package goal to create the WARs if you haven't already done so.

Rename the client WAR to concert-webapp.war, and the server WAR to webservice.war. This will prevent you from needing to make changes to Config.java and fetch-api.js in the client project. Alternatively, you may make the changes to these files as required.

Start the server running. (right-click it to get the option).

In a file explorer, browse to the server path / deploy path as in step 6 - except, locate the webapps folder, rather than wtpwebapps.

Copy / paste your WARs into the webapps folder. If the server is started, you should notice folders shortly being created by Tomcat. And, you can see Tomcat's logging output from the Eclipse console.

Browse to the appropriate URL from your browser (which should be http://localhost:10000/concert-webapp/ if you've followed along), and enjoy.

When you make modifications and repackage your WARs, you can delete the contents of the webapps folder and re-copy your new WARs over (while the server is stopped).
