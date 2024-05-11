## My First Vulnerable Machine Exploited for Root Perms

### Scanning with Nmap

I decided to download a beginner's machine to work on just to get my feet wet a bit on ethical hacking. I downloaded the Basic Pentesting 1 machine from VulnHub.
Running the machine on Virtual Box leads to a login screen on an Ubuntu device requiring a password.
I decided to just go ahead and use whatever I know about Nmap and see how far I could go before I was stuck.
The Kali machine I'm on and the vulnerable machine are set to be on the same network, so the first thing I did was to find the ip address of my machine.

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/7c599064-efbc-44aa-8a62-86f97bf07a24)

I can now scan the subnet for any other active hosts

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/ce9dd2ae-27d9-42ba-b1b3-cb7ea000c8d8)

The only other host on this network is x.114, so that must be the vulnerable machine
Now, I try and scan that device for any open ports I can investigate

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/7ff7dbf7-bd56-4cc1-8a1e-ae8728362b72)

I felt a little intimidated looking into web related ports, with how important and difficult "web application security" seems, so I decided to investigate the other two ports by finding out their versions

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/894ceb50-01e1-4427-a052-0601dc400def)

With this information, I can then look online for resources about vulnerabilities that may be present, in case any services are not up to date.
However, I can also use nmap's vulnerability script to scan those ports for vulnerabilities

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/47709040-939c-4ab2-b41b-f665ba324bb0)

It says that this installation has been backdoored with something called ftp-proftpd-backdoor, which I don't have any insight about.

### Exploiting with Metasploit

I don't have any experience with Metasploit, but while I was learning Nmap, I would see metasploit be mentioned a lot in being useful for exploiting vulnerabilites found with nmap, so I decided to introduce myself to the tool
I can search keywords of the exploit I am interested in, so for this I searched "proftpd" as that was port 21's service version and was also mentioned in the vulnerability

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/a8ba0ae7-3019-4924-80c0-769953ec1d01)

I decided to load the 5th exploit as that's the only one talking about a backdoor, so I thought that would be useful

Trying to run the exploit prompted me to set something called "RHOSTS", I learned this meant the target system, so I put in the ip address
I tried running again, but then this time it gave me an error, saying that "A payload was not selected"

After a quick google search on learning what a payload was, I searched for available payloads for this exploit

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/94e5d7c7-6efb-4ab0-b367-b2be0c4d1537)

I kind of just picked one at random here, picking #6
I then had to set the "LHOST" which I learned meant my, the attacker's, system
Now after hitting run, it had worked

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/c68d0959-29af-4c8e-8506-52974e96c962)

I have root access on the other machine and am able to control it just like how I would use a normal command line
This is where being super comfortable with using a CLI is critical, as this is pretty much the only way I can interact with the system

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/b32b6f19-82f8-4ac5-b025-196b6153dfb0)

Then, just out of curiosity, I wanted to see if I could do something like create a new user, and it actually worked, verifying that I did gain access to the system

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/56c50c9a-6548-44ab-a26c-65bd7dc181e5)

I can also change the password of the default user that was on the machine "marlinspike"
I had a bit of trouble changing the password, because I didn't know at the time that there were additional prompts that are usually associated with changing the password on a CLI, being "Enter the new password" then "Retype the password", but it was hidden in the metasploit console so I just assumed they were there.

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/eaae450f-0ee3-4d4d-8606-a09280de4e14)

I verified that the password did change by logging in on the other machine

![image](https://github.com/rat-v/Vulnerable-Machines/assets/169432484/f5a2641d-7f85-4a8f-863a-53484f47200c)

This was really exciting as this was my first ever machine that I actually worked on and successfully gained remote root access to. I had used my knowledge in Nmap and also spontaneously introduced myself to Metasploit to exploit a vulnerability I found.
This motivates me a lot, making me want to learn so much more. 


