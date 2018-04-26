Introduction - Provide a description of the product and what you were hired to do
	I was hired to find security issues in the ridesharing app, notuber. It consists of a clientside webpage with googlemaps api and sends and receives information with the server api at https://safe-everglades-73233.herokuapp.com/rides
Methodology - Describe your methodology pen testing the application, including the tools that you used
	I used chrome and curl. I started with blackbox testing and then downloaded the source code to look for more issues.
Abstract of Findings - Provide an overview of all the security and privacy issues you identified. This section should be written for non-technical managers who do not have technical expertise and do not have time to read the entire document. Write this section using lay language.
	The app has numerous security issues. The most glaring is that there is no user authentication -- it was very easy for me to impersonate a driver whose username I knew and update their location. Additionally, it is very easy to inject malicious script onto the server through the rides API -- meaning that the homepage on the server which displays passengers' requests can easily be manipulated to show fake content or do worse things.  
Issues Found - For each issue that you find, document:
Issue (e.g., database injection, really bad programming practice)
Location or page where issue was found
Severity of issue (e.g., low, medium , or high). Justify your answer.
Description of issue. How did you find it? A screenshot of problem is excellent.
Proof of vulnerability. Show pictures or it didn't happen.

Issue: Cross-site Scripting - through the /rides route, anyone can insert a script through the username field which will run on the / route. This is a high severity issue as it allows anyone to do anything to that page. A user who goes on that page could find themself downloading malware that was stored on the server. This problem is luckily very easy to solve. Sanitize your input. Make sure that any input from the user has special characters removed so that scripts injected like <script>alert("hacked")</script> cannot run.
Below I show a picture of the command I ran on curl to perform an attack and the result on the / route. Although my attack was mostly harmless, much worse things could be done.
![Using curl to inject javascript.](curl.png)
![Script is executed in browser.](log.png)
![Another injected script is executed in browser.](alert.png)
Issue: CORS access is given to everyone! You don't need to give this to everyone. You probably only want people accessing the API through your own interface anyway.

Conclusion - Consider adding user authentication so that users are not easily impersonated. Sanitize all user inputs to avoid cross-site scripting and query injection (although I was not able to perform a query injection successfully, it was because mongodb rejected my special character $; instead of relying on them you could more explicitly do this yourself)  

References - A list of references and links that you used for your work.
	None