## 📖 System Description
A booking service is required for a small venue, with a capacity of 120 seats. The venue’s seats are classified into three price bands: Silver, Gold, and Platinum.
Key requirements:
  * A concert may run on multiple dates, and each concert has at least one performer.
  * A performer may feature in multiple concerts.
  * Clients can:
    * Retrieve information about concerts and performers.
    * Enquire about available seats and reservations.
    * Authenticate to make reservations and view their own bookings.
  * Reservation rules:  
    * Clients can view available seats and their pricing.
    * No double-bookings are permitted.
    * Reservations must succeed in full (no partial bookings).
    * Only one client can book a specific seat for a specific concert/date.
  * Non-authenticated clients can view concerts, performers, and seat availability.
  * Authenticated clients can make reservations and view their own reservations only.  
  * Clients can subscribe to concert notifications (e.g., when a concert/date is about to sell out).
  * A critical quality attribute is scalability, as high load is expected when tickets go on sale.

## ▶️ Running The System
The system consists of a client project and a service project, both packaged into WAR files and deployed to a servlet container such as Tomcat.

### General Steps
1. Run Maven’s package goal on the parent project to build both WAR files.
2. Download and unzip Tomcat 8.5.x (archive version, not installer).
3. Set up Tomcat in your chosen IDE (IntelliJ Ultimate or Eclipse for Java EE Developers).

### Running in IntelliJ (Ultimate Edition only)
1. Open Run Configurations (Edit Configurations).
2. Click +, select Tomcat Server → Local.
3. Choose an available HTTP Port (e.g., 10000).
4. Configure the application server by pointing to your Tomcat installation.
5. Under the Deployment tab:
  * Add both WAR artifacts (client and service).
  * Set context paths:
  * Service WAR → ```/webservice```
  * Client WAR → ```/concert-webapp```
6. In the Server tab, set the URL to: ```http://localhost:10000/concert-webapp/```
7. Update configuration files if needed:
  * ```Config.java``` → ```check WEB_SERVICE_URI```
  * ```fetch-api.js``` → ```check WEB_URI```
8. From the configurations dropdown, select your Tomcat config and click Play.
9. Stop the server when finished (you may need to click Stop twice until disconnected).


### Running in Eclipse (Java EE Developers edition)
1. Go to Window → Preferences → Server → Runtime Environments.
2. Click Add, choose Apache Tomcat v8.5, and point to your unzipped installation.
3. Open the Run Configurations menu, locate Apache Tomcat, and create a new run config.
4. Open the Servers View (```Window → Show view → Servers```) and create a new Tomcat server.
5. Configure the server:
     * Set the HTTP/1.1 port (e.g., ```10000```).
     * Adjust the Server path and Deploy path if needed.
6. Run Maven’s ```package``` goal to create WARs (if not done already).
7. Rename WARs for convenience:
   * Client WAR → ```concert-webapp.war```
   * Service WAR → ```webservice.war``` (this avoids editing config files)
8. Start the server.
9. Copy both WARs into Tomcat’s ```webapps``` folder (e.g., ```.../wtpwebapps/webapps```).
10. Tomcat will expand the WARs automatically.
11. Open the app in your browser at: ```http://localhost:10000/concert-webapp/```
12. When modifying and repackaging WARs:
      * Stop the server.
      * Delete contents of the ```webapps``` folders.
      * Copy over the new WARs.
      * Restart the server.



