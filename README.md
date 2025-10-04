<h1><b>Java App and deploy with Maven and Apache Tomcat</b></h1>

<h2>1. Create a Simple Java Web App (Maven-based)</h2>

Prerequisites:
<ul>
<li>Java JDK 8 or later</li>
<li>Apache Maven installed</li>
<li>Git (optional, for version control)</li>
</ul>

<h2> 2. Set Up Jenkins Freestyle Maven Job</h2>
Prerequisites:

<ul> 
  <li>Jenkins installed (with Maven and Git plugins)</li>
<li>Apache Maven configured in Jenkins (Manage Jenkins → Global Tool Configuration)</li>
  </ul>
  
<h2>Steps:</h2>
1.	Create a new freestyle project:
   <ul><li>Go to Jenkins Dashboard → New Item → Enter name (my-webapp-build) → Select Freestyle project → OK.</li> </ul>
2.	Configure Source Code Management:
     <ul> <li>Select Git and enter your repository URL (https://github.com/yourusername/my-webapp.git).</li> </ul>
3.	Set Build Trigger (optional):
   <ul> <li>Enable Poll SCM (e.g., H/5 * * * * to check every 5 minutes).</li> </ul>
4.	Add Build Step:
     <ul> <li>Under Build, click Add build step → Invoke top-level Maven targets.</li>
      <li>Select your Maven installation (Maven 3.x).</li>
      <li>Enter goals: clean package.</li> </ul>
5.	Archive WAR file (optional):
    <ul><li>Under Post-build Actions, add Archive the artifacts.</li>
    <li>Enter **/*.war to save the WAR file.</li> </ul>
6.	Save & Run Build:
   <ul> 
    <li>Click Save, then Build Now.</li>
    <li>Verify the build succeeds and my-webapp.war is generated.</li> 
   </ul>
    
<h2>3. Deploy to Apache Tomcat</h2>
Prerequisites:
<ul> 
<li>Tomcat installed (http://localhost:8080/manager accessible)</li>
<li> Jenkins has the Deploy to container plugin installed.</li> 
</ul>
<h2>Steps:</h2>

1. Configure Tomcat Manager Access:
<ul> 
<li>	Edit conf/tomcat-users.xml:</li>
</ul> 

2.	Add Tomcat credentials in Jenkins:
<ul>
<li> Go to Manage Jenkins → Credentials → System → Global credentials → Add Credentials.</li>
<li>Choose Username with password: </li>
	Username: admin <br>
	Password: admin <br>
	ID: tomcat-creds (optional)
  </ul>
3.	Add Post-build Deployment in Jenkins:
<ul>
<li> Go back to your Jenkins job → Configure.</li>
<li> Under Post-build Actions, add Deploy war/ear to a container.</li>
<li> Configure:</li>
	WAR/EAR files: **/*.war (or target/my-webapp.war) <br>
	Context path: /my-webapp (leave empty for root /) <br>
	Containers: Select Tomcat 9.x and enter: <br>
	Manager credentials: admin:admin (or select from credentials) <br>
	Tomcat URL: http://localhost:8080
</ul>
  
4.	Run the Build Again:
<ul>
<li>	Jenkins will now deploy the WAR to Tomcat. </li>
<li> Verify at: http://localhost:8080/my-webapp/hello </li>

</ul>

<h1> Final Output </h1>

<b>•	Access your deployed app at:</b>

(http://<tomcat-server>:8080/my-webapp/hello)  <br>
You should see:
<b> "Hello from Jenkins & Maven!" </b>


