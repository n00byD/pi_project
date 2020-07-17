# pi_project

Steps to reproduce:

1. Set up Raspberry Pi with headless Raspian
2. SSH into RPi
3. Download libraries to RPi:

* ```sudo apt update -y && sudo apt upgrade -y```
* ```sudo apt install python3```
* ```sudo apt install python3-pip```
* ```sudo apt install git vim -y```
* ```pip3 install RPi.GPIO```
* ```pip3 install requests```
* ```pip3 install json```
* ```pip3 install base64```

4. Clone git repository to RPi:

    ```git clone https://github.com/joshwh11/pi_project```

5. Set up breadboard with Raspberry Pi. Requires:
* Breadboard
* 3x Female-to-Male wires
* 2x LED Pins (1 red, 1 yellow)
* 2x 220Ω Resistors 

    (Super rough diagrams for reference are in the "schematic" folder)

6. Test out pins by running the ledtest.py file after changing directory to the pi_project folder:

    ```cd pi_project```
    
    ```python3 ledtest.py```
    
7. Now that the lights are working, let's set up a GitHub repository to hold the file that AppDynamics will update if a policy is triggered. Create an account if
   you do not already have one and create a repo with one file named "syntheticHealth.txt" that contains simply a 0. 0 will be the default "off" state of the LED. 
   If a policy is triggered, AppDynamics will update the file to a 1, or "on" state. Also, you will need a token to authenticate any request to update a GitHub 
   file. To generate a token, click on the icon drop-down at the top right of GitHub page after logging in -> Click "Settings" -> Click "Developer settings" -> 
   Click "Personal access tokens" -> Click "Generate new token"

8. Set up AppDynamics policy and action.
    
9. To update the LED pins, the RPi will be continuously running the checkHealth.py application as AppDynamics updates the syntheticHealth.txt file via policy 
   triggers. On your RPi, navigate to pi_project on your RPi and run checkHealth.py via
   
   ```python3 checkHealth.py```
   
   Now the RPi will constantly checking the contents of your syntheticHealth.txt file and should update the LED pin state given the content of the file.
