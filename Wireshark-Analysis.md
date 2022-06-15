## Wireshark Strikes Back


#### Time Thieves

At least two users on the network have been wasting time on YouTube. Usually, IT wouldn't pay much mind to this behavior, but it seems these people have created their own web server on the corporate network. So far, Security knows the following about these time thieves:

- They have set up an Active Directory network.
- They are constantly watching videos on YouTube.
- Their IP addresses are somewhere in the range `10.6.12.0/24`.

You must inspect your traffic capture to answer the following questions in your Network Report:
1. What is the domain name of the users' custom site?
  - Found after plenty of research:
  - Given that they have set up an active directory network, I decided to look specifically for packets with Kerberos. The active directory network will use Kerberos for authentication.
    - To do this I filtered by kerberos.crealm. I chose crealm, as we know they're using a specific domain name.
  - The only kerberos crealm that appears in the IP range is frank-n-ted.com.
2. What is the IP address of the Domain Controller (DC) of the AD network?
  - It appears that the IP address is 10.6.12.12
3. What is the name of the malware downloaded to the 10.6.12.203 machine?
  - 10.6.12.203 made a GET HTTP request for a file called june11.dll. This appears to be the malware.

4. Upload the file to [VirusTotal.com](https://www.virustotal.com/gui/). 
5. What kind of malware is this classified as?
  - Virus total classifies it as a trojan.

#### Vulnerable Windows Machines

The Security team received reports of an infected Windows host on the network. They know the following:
- Machines in the network live in the range `172.16.4.0/24`.
- The domain mind-hammer.net is associated with the infected computer.
- The DC for this network lives at `172.16.4.4` and is named Mind-Hammer-DC.
- The network has standard gateway and broadcast addresses.

Inspect your traffic to answer the following questions in your network report:

1. Find the following information about the infected Windows machine:
  - All traffic coming from 172.16.4.4, which we know is the DC for this network is going to the same computer. That one computer's info is:
    - Host name: ROTTERDAM-PC (Found in NBNS packets from this IP address.)
    - IP address: 172.16.4.205
    - MAC address: 00:59:07:b0:63:a4
    
2. What is the username of the Windows user whose computer is infected?
  - According to the Kerberos packets, the username appears to be matthijs.devries
3. What are the IP addresses used in the actual infection traffic?
  - The majority of the traffic moving in and out of this pc is being sent to 185.243.115.84, so it is likely there.
4. As a bonus, retrieve the desktop background of the Windows host.


#### Illegal Downloads

IT was informed that some users are torrenting on the network. The Security team does not forbid the use of torrents for legitimate purposes, such as downloading operating systems. However, they have a strict policy against copyright infringement.

IT shared the following about the torrent activity:

- The machines using torrents live in the range `10.0.0.0/24` and are clients of an AD domain.
- The DC of this domain lives at `10.0.0.2` and is named DogOfTheYear-DC.
- The DC is associated with the domain dogoftheyear.net.

Your task is to isolate torrent traffic and answer the following questions in your Network Report:

1. Find the following information about the machine with IP address `10.0.0.201`:
    - MAC address 00:16:17:18:66:c8 
    - Windows username: elmer.blanco (from kerberos packets) 
    - OS version: BLANCO-DESKTOP (also from kerberos packets)

2. Which torrent file did the user download?
    - Found by finding the first chronological packet with the BitTorrent protocol, and looking at HTML requests that happened shortly before it. A couple GET requests up is one for a bit torrent download for a file called Betty_Boop_Rhythm_on_the_Reservation.avi.torrent. What an odd thing to torrent.


---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  
