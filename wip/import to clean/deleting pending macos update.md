In Mac Os version 10.5 I couldn't update to a newer minor version. Everytime i hit the update button in the settings a new update was downloaded. Only after trying to install the Mac just rebooted. After a while my harddrive got full so i had to get rid of the update files. 

Unfortunately it's not possible to remove the update files directly from the filesystem, because it's protected by default.

1.  Restart your mac and Keep **⌘** + R pressed until you see the startup screen.
2.  Open the terminal in the top navigation menu.
3.  Enter the command 'csrutil disable'. _This command gives unrestricted access to every folder the OS._
4.  Restart your Mac
5.  Go to the /Library/Updates folder in the finder and move them to the bin.
6.  Empty the bin.
7.  Repeat step 1 + 2
8.  Enter the command 'csrutil enable' to activate protection.
9.  Restart you Mac.
10.  To be sure you can check if the proctection correctly activated with the 'crustil status' command.