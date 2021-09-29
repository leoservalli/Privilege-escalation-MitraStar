# Privilege-escalation-MitraStar
Privilege escalation vulnerability on MitraStar routers

Device: Mitrastar GPT-2541GNAC-N1
Firmware: BR_g3.5_100VNZ0b33

Exploit: 

Mitrastar GPT-2541GNAC-N1 devices are provided with access through ssh into a restricted default shell:

![image](https://user-images.githubusercontent.com/90664730/135199877-45d8965a-5068-4cc5-ac26-6d600039932f.png)


That restricted shell has CLI Version “Reduced_CLI_HGU_v15”, and the environment is restricted to avoid execution of common linux/unix commands.

![image](https://user-images.githubusercontent.com/90664730/135199655-c22019d8-a417-471d-baa6-3780599548cc.png)

The command “deviceinfo show file <path>” is supposed to be used from reduced CLI to show files and directories. Because this command do not handle correctly special characters, is possible to insert a second command as a parameter on the <path> value. By ussing “&&/bin/bash” as parameter value we can spawn a bash console, as seen on the next image:

![image](https://user-images.githubusercontent.com/90664730/135199703-c8b56776-f413-4ad4-ac45-9f94b0d39d70.png)


So it is possible to escalate privileges by spawning a full interoperable bash console with root privileges (see next image):

![image](https://user-images.githubusercontent.com/90664730/135199738-2e009197-fce1-4ee3-9513-07c711c3a67f.png)


Through this escalation is possible change the content of /etc/passwd (/var/passwd), create new users, or change any other system resource.

The user “support” who has root privileges, is provided printed on the back of the router. As reported on a previous CVEs (CVE-2017-16523 / CVE-2017-16522), some Mitrastar routers use default user and passwords that have permission to connect through SSH.



