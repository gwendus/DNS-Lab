<p align="center">

<img src="https://journeyofthegeek.com/wp-content/uploads/2019/11/azure-dns.png?w=512&h=476&crop=1"  height="30%" width="30%" alt="Group Policy Management Console"/>
 
 <h1>Domain Name System Lab</h1>
The objective of this lab is to gain hands-on experience with the role of DNS in networking, focusing on its function in translating domain names to IP addresses and its integration within a cloud-based environment. This lab relies on our resources created in our previous networking lab.

<br />


<h2>Environments and Technologies</h2>

- <b>Microsoft Azure</b> 
- <b>Remote Desktop</b>
- <b>Ping</b>

<h2>Operating Systems</h2>

- <b>Windows 10</b> (22H2)
- <b>Windows Server</b> (2022)
  <br />

<h2>Prerequisites</h2>
Complete the following lab series: <a href="https://github.com/gwendus/ADInfrastructureInAzure/blob/main/README.md">Preparing Active Directory Infrastructure in Microsoft Azure</a>
<br />

<h2>Address-Record Exercise</h2>
Log into DC-1 as jane_admin (your domain admin account) and then log in to Client-1 as an admin too. From Client-1, try to ping "mainframe" and notice that it fails.
  <br>
  <br>
<img src="https://i.imgur.com/ejtxKGi.png" height="80%" width="80%" alt="ping mainframe"/>
<br />
<br />

Nslookup "mainframe" and notice that it fails.


<img src="https://i.imgur.com/IFtlZYw.png" height="80%" width="80%" alt="nslookup mainframe"/><br />
<br />
<br />

Create an Address-Record or A-Record on DC-1 for "mainframe" and have it point to DC-1's Private IP address. First, open DNS Manager, then navigate to DNS>DC-1>Forward Lookup Zones>mydomain.com.

<img src="https://i.imgur.com/SeUKA1J.png" height="70%" width="70%" alt="navigate to create a record"/>

<br />
<br />

Right click and select "New Host (A or AAA)
 <br/>

<img src="https://i.imgur.com/V9VoTd0.png" height="70%" width="70%" alt="New A record"/>
<br />
<br />

Under New Host, we will now create a record for the term "mainframe" and enter the Private IP address associated with DC-1. Click "add host." <br>
<br />
<img src="https://i.imgur.com/6nDLU6H.png" height="40%" width="40%" alt="add host"/>

<br />
<br />

Go back to Client-1 and try to ping it. Observe that it works
  <br>
<br/>
<img src="https://i.imgur.com/kK48WhS.png" height="80%" width="80%" alt="a-record created"/>
<br />
<br />
<h2>Local DNS Cache Exercise</h2>
Go back to DC-1 and change mainframe’s record address to 8.8.8.8
<br/>
<img src="https://i.imgur.com/6PCTpct.png" height="60%" width="60%" alt="8.8.8.8"/>
<br />

Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address
 <br/>

<img src="https://i.imgur.com/kK48WhS.png" height="80%" width="80%" alt="ping dns again"/>
<br />
<br />

Observe the local dns cache (ipconfig /displaydns). We will open it in a text file. <br/>

<img src="https://i.imgur.com/B2j4AM1.png" height="80%" width="80%" alt="displaydns"/>
<br />
<br />
<img src="https://i.imgur.com/b61U1Bj.png" height="80%" width="80%" alt="displaydns2"/>
<br />
<br />

Flush the DNS cache (ipconfig /flushdns). <br/>

<img src="https://i.imgur.com/D0cyKC2.png" height="80%" width="80%" alt="flushdns"/>
<br />
<br />

Observe that the cache is empty (ipconfig /displaydns) <br/>

<img src="https://i.imgur.com/nJRnLNY.png" height="80%" width="80%" alt="displaydns"/>
<br />
<br />

Attempt to ping “mainframe” again. Observe the address of the new record is showing up <br/>

<img src="https://i.imgur.com/0uPdkRW.png" height="80%" width="80%" alt="new record showing"/>
<br />
<br />

<h2>CNAME Record Exercise</h2>

Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com" <br/>

<img src="https://i.imgur.com/oOZF3rq.png" height="60%" width="60%" alt="create cname"/>
<br />
<br />
<img src="https://i.imgur.com/JJkgeiW.png" height="60%" width="60%" alt="create cname2"/>
<br />
<br />

Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record <br/>

<img src="https://i.imgur.com/Z8R8i1F.png" height="80%" width="80%" alt="Ping search"/>
<br />
<br />

On Client-1, nslookup “search”, observe the results of the CNAME record <br/>

<img src="https://i.imgur.com/b9MWv3q.png" height="80%" width="80%" alt="nslookup search"/>
<br />
<br />
