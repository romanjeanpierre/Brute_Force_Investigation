<h1> Brute Force Investigation</h1>

<h2>Brief Description</h2>
<p> This project involves a critical investigation into a brute force attack on our website, aimed at identifying the attack's origin, its success rate, and the extent of access gained by the attacker. Given the high urgency of the situation, a swift and thorough analysis is paramount to mitigate potential risks to our server systems. </p> 

<p> The complexity of this investigation requires a multifaceted approach, analyzing various log types to piece together the sequence of events. Our focus includes scrutinizing the administrator URL (http://imreallynotbatman.com/joomla/administrator/index.php) and tracking HTTP POST requests for username and password submissions. The primary objectives are to pinpoint the attack's source swiftly, determine the breach's success, and understand the actions taken by the intruder post-access. </p>
    
<h2>Project Walk-Through</h2>

<h3> Identify how many events relating to Login activity</h3>
<p> Command => <code> index"botsv1" sourcetype="stream:http" http_method=POST uri="/joomla/administrator/index.php"</code></p>
<img src="https://imgur.com/eIPxvbt.png" height="80%" width="80%" alt="FTK Imager Memory Capture">
<p> Results = 425 Events</p>

<h3> Scroll to "src_ip" under interesting fields column on the left</h3>
<p> Determine majority traffic volume from single IP address</p>
<img src="https://imgur.com/lCAYyyz.png" height="80%" width="80%" alt="FTK Imager Memory Capture">
<p> 23.22.63.114 with recent 412 events </p>

<h3> Verify destination IP Address of web server domain </h3>
<img src="https://imgur.com/Qp7RYyI.png" height="80%" width="80%" alt="FTK Imager Memory Capture">

<h3> Determine brute force credentials used to brute force on specific date & time</h3>
<p> Command => <code>index"botsv1" sourcetype="stream:http" http_method=POST uri="/joomla/administrator/index.php" src_ip="23.22.63.114" | spath timestamp | search timestamp=="2016-08-10T21:46:44.453730Z" </code> </p>
<p> Exapnd packet details > Scroll to SRC_CONTENT </p>
<img src="https://imgur.com/xGmJDaz.png" height="80%" width="80%" alt="FTK Imager Memory Capture">

<h3> Improve Brute Force credentials representation </h3>
<p> <code>index"botsv1" sourcetype="stream:http" http_method=POST uri="/joomla/administrator/index.php" src_ip="23.22.63.114" | table timestamp, form_data | sort -time asc </code></p>
<img src="https://imgur.com/OA96RSS.png" height="80%" width="80%" alt="FTK Imager Memory Capture">

<h3> Conclusion</h3>
<p> The investigation into the brute force attack on our website has been comprehensive and revealing. We successfully identified the source of the attack, and determined the extent of its success. Our analysis, which involved a detailed examination of various log types, particularly focused on HTTP POST requests at the administrator URL, provided critical insights. Despite the complexity and urgency of the task, our methodical approach enabled us to effectively mitigate the risks posed to our server systems.</p>
