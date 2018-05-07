Jeff Beeby

Guy Verrier

ETR 164

IRC Server Documentation

As stated in my propsal, the goal of this project is to create an IRC Server. With that I used a raspberry pi 3 for this project, giving myself knowledge that I will be using in my final project. 

My personal objectivas are as follows:
  ~First I needed to understand what an IRC Server was and what it did.
  ~Second I would need to know how to set up a Raspberry Pi.
  ~Third learn how to burn an ISO file to a SD card
  ~Fourth I need to find the software needed to do this
  ~Fifth I need to set it up and see if it actually worked
  
With this project I am a little behind the 8 ball for that fact that my knowledge with linux is lacking. Knowing this I used that aif of 3 websites to actually acomplish this project so do not that my steps are just a summary of what they state just in my own short hand. So again if you want to know the steps more in depth please visit the web site I state.

Part 1 Setting up Raspberry Pi with Noobs OS:
(Used this site for the set up: https://www.raspberrypi.org/help/noobs-setup/2/)

First I had to get the parts needed:
- Raspberry Pi 3
- Power source (same as any android phone using a micro usb connection)
-micro sd card (8gb minimum) with adapter
-HDMI card
-Monitor 
-Wired Mouse and Keyboard
-Decktop/laptop that you can download files off the interent with

Second I then Downloaded the Noobs Zip File. Do note that its over 1 GB in size so make sure you have a reliable connection

Third, while that is downloading Format your SD Card so it is all ready when the file is downloaded.

Fourth, extract the files from the Zip folder and then Drag and drop them to the formatted SD Card

Fifth, slide the micro SD card in the pi, plug the HDMI cable up to the monitor and into the slot on the Pi. Plug in the mouse and keyboard and when its all read plug in the power supply.

Sixth, since this is the first boot, a window will appear asking which OS you want to install. I used Raspbian, and clicked install. After it is installed a configuration page will appear (raspi-config) so you can set time and date. Tab to finish.

Seventh, defualt login is "pi" with password "raspberry" To load the graphical user interface type startx and press enter

Part 2: Setting up the IRC Server
(Used this site for the set up: https://pimylifeup.com/raspberry-pi-irc-server/)

First: Before you do anything else, and assuming you just finished part 1, we need to make sure everything is up to date with the OS on the Pi so. Open a Terminal (ctrl + T for the short cut but i just used the menu bar myself) and type "sudo apt-get update". Let that run then once its done type "sudo apt-get upgrade". This just updates and installs  any software you have on your Pi currently.

Second: Next we will download a program called Ircd-Hybrid. We can do this straight from the command line so with the terminal still open type "sudo Apt-get install ircd-hybrid". Just remember these commands are case sensative and must be spelled correctly so be careful; that is the #1 cause for most errors when doing this.

Third: The server requires a password, type" /usr/bin.mkpasswd password"
(please not the word password is what evere you want your password to be; but make sure you remember it or else you wont be able to connect to your irc server)

Fourth: Next we will need to modify a file straigh from the command line. Type "sudo nano /etc/ircd-hybrid/ircd.conf"
  A) This will open the file and we are looking for "serverinfo {block". 
    1) Find "name = "hybrid8.debian.local";" and replace it with "name = "pimylifeup.irc";"
    2) NOTE! This defines the name of your IRC server, you can set it to whatever you want.
    3) Find "description = "ircd-hybrid 8.1-debian";"   Replace with "description = "Raspberry Pi IRC Server";" (This sets the                    servers description and will be what people see when they connect to your server.)
    4) Find "network_name = "debian";
                    network_desc = "This is My Network";"
              Replace with "network_name = "pimylifeup";
                            network_desc = "This is my Raspberry Pi IRC Network";"   (This is for describing the name and description of                              the network that your server is on)
    5) Find "max_clients = 512;" Replace with "max_clients = 128;" (This defines the maximum amount of people that can be                     connected to the IRC Server)
   B)Now within "operator { block"
    1)Find and remove "#" (This section requires uncommenting, remove the first layer of #, if you see ## only remove the first one)
    2) Find "name = "sheep";" Replace with "name = "op";" (This defines the name of the operator group, we will use op as it is easiest       to remember, you can set this to whatever you want)
    3) Find "user = "*@192.0.2.240/28";" Replace with "user = "*@*";" (This will change it so that anyone connecting to the server can run the oper command. If you want to restrict this to local users only you can try using something like “*@192.168.*.*“.)
    4) Find "password = "xxxxxxxxxxxxx";" Replace with "password = "REPLACE WITH YOUR ENCRYPTED PASSWORD";" (Here we will want to replace the default password with the one that we encrypted earlier in the tutorial with the /usr/bin/mkpasswd tool. Remember this is not the plain text version of your password, it is the scrambled form.)
    
Fifth: Now we can save and quit out of the file by pressing Ctrl +X then pressing Y and then Enter.
Sixth: With that now done you can modify the message of the day (MOTD) for the IRC Server. This is fairly easy to modify as the ircd-hybrid software reads it from a file called ircd.motd that is located in the /etc/ircd-hybrid folder.
  A) You can begin modifying this file by running the following command in terminal: "sudo nano /etc/ircd-hybrid/ircd.motd"
  B) I just kept it simple just to make sure I was able to connect to it.
Seventh: Now we want to restart the software to update all the changes; in the command terminal type "sudo /etc/init.d/ircd-hybrid          restart"

Part 3: Connecting to your IRC Server
For the next part use the other Desktop or Laptop from before when you downloaded the noobs file. My machine was Linux so ill be going off of that.
First: Download mIRC and install it; I used this link: https://www.mirc.com/
Second: Once done installing, open the program and do the following:
  A) File > Select Server
  B) Click "Add" from the new window
  C) On the newest window fill in the Description and Address text boxes. make description unique so it stands out. for the address use the ip address of your raspberry pi. (to find this out, go to the pi and in the command terminal type "hostname -l". it will be in there) 
  D) Click "Add"
  E) Your server should now be added to mIRC’s list of IRC servers. It should also now already be selected, if it isn’t look for your new addition, it will be under the name you set for “Description:”.
  F) Once you are certain you have it selected, press the “Select” button.
  G) You will finally be brought to one final screen before making the connection, here you will want to set your “Nickname:” to whatever you want. Now before you jump ahead and press the “Connect” button make sure your server description name is next to “Server:”
  H) Once you are sure it is correct, click the “Connect” button.
  I) Finally, type in the channel name you want to use, this can be anything as long as it starts with a #, once typed in all you need to do is click the “Join” button.
Third: If all has gone well you should now be successfully connected to your Raspberry Pi IRC Server.

I really learned alot with this project; from setting up a Pi to what an IRC server really is. This was alot of fun and I hade a great time doing this.

In conclusion, the process of creating the server was fairly straightforward. The only problems I encountered was when I was trying to set up the Super User so i can make this IRC more secure. After some additional research I found the coding ndded to do this but to be honest I dont forsee myself using my own personal IRC Server in this matter so I kept the information but did not impliment it.

Work Cited

https://en.wikipedia.org/wiki/Internet_Relay_Chat
https://pimylifeup.com/raspberry-pi-irc-server/
https://www.raspberrypi.org/help/noobs-setup/2/
