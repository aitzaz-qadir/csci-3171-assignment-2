# CSCI 3171 (Summer 2021) Assignment 2

* Name: Aitzaz Qadir Khowaja
* Date: 21st July ' 2021
* B00 : 853169
* Dal E-mail: at382154@dal.ca

## How to Run

>Description

1. To run the program, navigate to the "code" or "Bonus_Code" folder inside terminal or command line using cd commands.
Open two terminals, one for the server and one for the client.

2. First, run the server side with command similar to "python3 Server.py [host port]"
Host Port number can be any number > 1024 , I tested the program using 8800. So my command was "python3 Server.py 8800"

3. Then, run the client side with command similar to "python3 ClientLauncher.py [host name] [host port] [rtp port] movie.Mjpeg"
Host name is the name of the machine being used, in case of Linux it is the name next to the @ in the terminal.
For example if terminal starts with "user@test-machine" then –> host name will be "test-machine".
I tested the program in Ubuntu Virtual box and my host name was "aitzaz-VirtualBox".

4. In my testing I usually set the rtp port to (host port) + 1 so in this case I used 8801. It can also be any free port number.
Hence my command was "python3 ClientLauncher.py aitzaz-VirtualBox 8800 8801 movie.Mjpeg".

>Troubleshooting

Your program may run into some issues if your system is missing key installations. In my testing I found problems with tkinter and Pillow to be most common.

* If tKinter is not recognized, use command "sudo apt-get install python3-tk".

* If Pillow is missing, use commands "python3 -m pip install --upgrade pip" and "python3 -m pip install --upgrade Pillow" to get the latest versions.

## Program Description

The programming was done using the starter code provided in python. Majority of the starter code remains untouched. Main work and changes were done in "Client.py" and "RtpPacket.py".

In Client.py, I completed the code for the sendRtspRequest's if statements regarding updating the seqNum at each request and formatting a rtp request in string.

The formatting was done by following the client requests and server responses examples given in the assignment document. Only the setup was formatted with full rtp header and the rest of the requests only had session. After that, the requestsent was updated to represent the correct request.

At the end the formatted request was encoded and sent through the socket. Further work was done in parseRtspReply, where the states were updated after every change according to the state diagram in the assignment document.

Finally in openRtpPort, I started a new socket and set the timeout to 0.5s as instructed. In RtpPacket.py, work was done to fill the byte array with bit values exactly as asked in the diagram given.

I ran into issue with the sequence number (header2) where the server would drop the connection at seq 256 since the max range was (0-255). But the issue was fixed using the 16 bit integer example from the document. At the end, the new header and payload was updated.

After submitting this version, I began working on Part-C and the bonus part. I calculated some statistics including packet loss and video data rates using what I had learned in assignment 1 and the time module. For the bonus part, I commented out all the code regarding the creation and functionality of the SETUP button. I shifted its function to occur directly after the server connects to the socket. I then renamed the TEARDOWN button to STOP accordingly.

## Program Design

The program is written in python and uses sockets and tkinter to produce a video streaming GUI with the ability to pause, play and stop the video stream. This video data was sent with RTP and RTSP protocols.

Most of the code for the GUI and streaming was prepared already, and design for remaining parts was provided in the assignment document which I followed. I used the time module for my statistic calculations.

## Submission Notes

I completed the regular section and Bonus section! I did run into troubles when testing the code since I was using Ubuntu 20.04 LTS on windows which is WSL. This made it so I couldnt access the GUI.

I found a way around this with a module called Xming which would provide a x-window display environment for the GUI. However, after research and help from the TAs I was able to correctly test the program on windows using CMD and on Ubuntu Terminal using a virtual machine.

The runfile.txt contains the exact commands I used for testing.

## Attributions and References

References here, according to the Dalhousie Academic Integrity Standards.

* https://www.dal.ca/dept/university_secretariat/academic-integrity/plagiarism-cheating.html
* https://www.dal.ca/faculty/computerscience/graduate-programs/grad-handbook/academic-integrity.html
* https://pillow.readthedocs.io/en/stable/
* https://docs.python.org/3/library/tkinter.html
* https://stackoverflow.com/questions/38181710/tkmessagebox-no-module/38181986
* https://askubuntu.com/questions/993225/whats-the-easiest-way-to-run-gui-apps-on-windows-subsystem-for-linux-as-of-2018
* https://docs.python.org/3/library/time.html#time.time

