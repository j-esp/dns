![image](https://github.com/user-attachments/assets/44f0c082-8ab8-4504-b923-4e5211fa5261)

<h1>DNS Management in Azure</h1>
As a fundamental IT concept, this activity focuses on DNS and its applications. Building on the previous task, I am logged into an administrator account, Jane Doe, on both VMs configured for Active Directory.

<h2>Technologies and Platforms</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Active Directory Domain Services
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Windows Server 2022

<h2>DNS Configuration</h2>

![image](https://github.com/user-attachments/assets/f7da4e46-eefd-4734-8c7a-fafd34ed4ece)
![image](https://github.com/user-attachments/assets/c34e319b-5e29-4b1c-a3b9-a4603595720f)
![image](https://github.com/user-attachments/assets/eb4b06f5-f2a2-492a-8c46-19189074119c)
![image](https://github.com/user-attachments/assets/80572265-f8e3-414e-b24a-57a1d2f2a83a)

<p>
After attempting to ping 'mainframe' and using 'nslookup mainframe,' we observed that both fail due to the absence of a DNS record. To resolve this, a DNS-A record must be created on the domain controller. This is done by opening the DNS Manager and navigating to the domain under the Forward Lookup Zones tab (in this case, conjuring.com). By creating a New Host record for 'mainframe,' which shares the same IP address as the domain controller, the ping now resolves successfully. Refreshing the DNS cache with ipconfig /flushdns ensures the new record is updated, and 'mainframe' is then resolved correctly.
</p>

![image](https://github.com/user-attachments/assets/270f42e2-e62c-4c75-a3af-c0d43233a93d)
![image](https://github.com/user-attachments/assets/22f2f4b0-0ffd-428a-9634-06636db5ba6c)
![image](https://github.com/user-attachments/assets/30e40144-3962-4b1c-82f5-d23633c4e58b)
![image](https://github.com/user-attachments/assets/4d3e210f-cde0-4f56-8042-81a59490e0b1)

<p>
This exercise demonstrates DNS cache management. On the domain controller, I updated the IP address for 'mainframe' to 8.8.8.8 (Google) and refreshed the DNS server. Initially, pinging 'mainframe' resolves to the old IP address, which can be confirmed using ipconfig /displaydns. To update the DNS cache, it is essential to clear it by running ipconfig /flushdns. After clearing the cache, pinging 'mainframe' will resolve to the new IP address.
</p>

![image](https://github.com/user-attachments/assets/15153e51-6066-4139-b692-3bf3e0d9ebeb)
![image](https://github.com/user-attachments/assets/8c4ade62-2b72-4f2c-a216-cfaaaa410db4)
![image](https://github.com/user-attachments/assets/ca9c8db2-f8eb-4029-8c7e-a628de674d55)
![image](https://github.com/user-attachments/assets/69956b83-4182-49fc-942e-444ad4f56423)

<p>
A CNAME record will now be made on the DNS server that will point "search" to Google. On Next, I will create a CNAME record on the DNS server to direct "search" to Google. In the DNS Manager, navigate to the Forward Lookup Zones tab, select the domain, and create a new CNAME record named "search" that points to Google. After creating the record, refresh the server to apply the changes.

It is important to ensure that root hints are correctly configured on the DNS server to enable resolution of external domains. Root hints provide the DNS server with the IP addresses of the root DNS servers, allowing it to resolve queries for domains not within the local DNS zone.

On the client, use ping search and nslookup search to verify that the CNAME record is resolving correctly. The results should reflect the CNAME redirection to Google. If the expected results are not seen, check the root hints configuration and refresh the DNS server cache as needed.
</p>
<br />

<h2>Key Takeaways</h2>
This activity enhanced my understanding of DNS implementation within a host and its network. DNS records can change, potentially causing connectivity issues, and clearing the DNS cache may be necessary to apply new records. The ipconfig /flushdns command is a critical tool in troubleshooting and is frequently used in IT.
