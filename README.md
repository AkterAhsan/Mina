মিনা  -- ভার্চুয়াল এসিস্টেন্ট রাসবেরী পাই বোর্ডের জন্য।

পাই জিরো এর জন্য এই রিপজি্টরী ব্যবহার করুন।। (https://github.com/warchildmd/google-assistant-hotword-raspi)

ফিচার:

1. একাধিক কাস্টম wakeword অ্যাক্টিভেশন ট্রিগার, সঙ্গে বুট শুরু হেডলেস অটোস্টার্ট।
2. IFTTT,api.ai, Actions SDK ছাড়া GPIO- র ভয়েস কন্ট্রোল।
3. ভয়েস কন্ট্রোল এর মাধ্যমে RPi GPIO- এর সাথে সংযুক্ত সার্ভো মোটর কন্ট্রোল। 
4. ভয়েস কমান্ড ব্যবহার করে সেফ শাটডাউন।
5. ইউটিউব থেকে মিউ্জিক স্ট্রিম করা।
শোনা ও বলার সময় নির্দেশক লাইট।
7. wakeword সনাক্তকরণের জন্য স্টার্ট আপ অডিও এবং অডিও ফিডব্যাক।

নুতুন যেসব ফিচার আসছে:

1. Mute করার বাটন.
2.গুগল হোমের মত নিও্পিক্সেল ইন্ডিকেটর.

এই প্রোজেক্টটি পাইথন ২ তে করা, কিন্তু অরিজিনাল গুগল এসিস্টেন্ট পাইথন ৩ তে করা, তাই কেউ যদি আগের গুগল এসিস্টেন্ট ব্যবহার করতে চান তাহলে হবে না।
তাই এক কপি ফ্রেস লেটেস্ট Raspbian Stretch আইএসও ব্যবহার করুন।


১ম ধাপ এই রিপজিটরিটি ক্লোন করুন এর জন্য
আপনার পাইের টারমিনাল ওপেন করুন এবং নিচের কমান্ডটি এক্সিকিউট করুন।
git clone https://github.com/AkterAhsan/Mina

INSTALL AUDIO CONFIG FILES

Update OS and Kernel
sudo apt-get update  
sudo apt-get install raspberrypi-kernel  
Restart Pi

Choose the audio configuration according to your setup.
(Run the commands till you get .bak notification in the terminal)

3.1. USB DAC or USB Sound CARD users,

sudo chmod +x /home/pi/GassistPi/audio-drivers/USB-DAC/scripts/install-usb-dac.sh  
sudo /home/pi/GassistPi/audio-drivers/USB-DAC/scripts/install-usb-dac.sh 
3.2. AIY-HAT users,

sudo chmod +x /home/pi/GassistPi/audio-drivers/AIY-HAT/scripts/configure-driver.sh  
sudo /home/pi/GassistPi/audio-drivers/AIY-HAT/scripts/configure-driver.sh  

sudo chmod +x /home/pi/GassistPi/audio-drivers/AIY-HAT/scripts/install-alsa-config.sh  
sudo /home/pi/GassistPi/audio-drivers/AIY-HAT/scripts/install-alsa-config.sh  
3.3. USB MIC AND HDMI users,

sudo chmod +x /home/pi/GassistPi/audio-drivers/USB-MIC-HDMI/scripts/install-usb-mic-hdmi.sh  
sudo /home/pi/GassistPi/audio-drivers/USB-MIC-HDMI/scripts/install-usb-mic-hdmi.sh  
3.4. USB MIC AND AUDIO JACK users,

sudo chmod +x /home/pi/GassistPi/audio-drivers/USB-MIC-JACK/scripts/usb-mic-onboard-jack.sh  
sudo /home/pi/GassistPi/audio-drivers/USB-MIC-JACK/scripts/usb-mic-onboard-jack.sh 
3.5. CUSTOM VOICE HAT users,

sudo chmod +x /home/pi/GassistPi/audio-drivers/CUSTOM-VOICE-HAT/scripts/custom-voice-hat.sh  
sudo /home/pi/GassistPi/audio-drivers/CUSTOM-VOICE-HAT/scripts/custom-voice-hat.sh  

sudo chmod +x /home/pi/GassistPi/audio-drivers/CUSTOM-VOICE-HAT/scripts/install-i2s.sh  
sudo /home/pi/GassistPi/audio-drivers/CUSTOM-VOICE-HAT/scripts/install-i2s.sh 
Those Using HDMI/Onboard Jack, make sure to force the audio

sudo raspi-config  
Select advanced options, then audio and choose to force audio

Those using any other DACs or HATs install the cards as per the manufacturer's guide and then you can try using the USB-DAC config file after changing the hardware ids

Restart Pi

Check the speaker using the following command

speaker-test -t wav  
CONTINUE after SETTING UP AUDIO

Download credentials--->.json file (refer to this doc for creating credentials https://developers.google.com/assistant/sdk/develop/python/config-dev-project-and-account)

Place the .json file in/home/pi directory

Rename it to assistant--->assistant.json

Using the one-line installer for installing Google Assistant and Snowboy dependencies
Pi3 and Armv7 users use the "gassist-installer-pi3.sh" installer and Pi Zero, Pi A and Pi 1 B+ users use the "gassist-installer-pi-zero.sh" installer. Snowboy installer is common for both
4.1 Make the installers Executable

sudo chmod +x /home/pi/GassistPi/scripts/gassist-installer-pi3.sh
sudo chmod +x /home/pi/GassistPi/scripts/gassist-installer-pi-zero.sh
sudo chmod +x /home/pi/GassistPi/scripts/snowboy-deps-installer.sh  

4.2 Execute the installers (Run the snowboy installer first. Don't be in a hurry and Don't run them parallely, Run them one after the other

sudo  /home/pi/GassistPi/scripts/snowboy-deps-installer.sh
sudo  /home/pi/GassistPi/scripts/gassist-installer-pi-zero.sh
sudo  /home/pi/GassistPi/scripts/gassist-installer-pi3.sh  

Copy the google assistant authentication link from terminal and authorize using your google account

Copy the authorization code from browser onto the terminal and press enter

Move into the environment and test the google assistant according to your board

source env/bin/activate  
google-assistant-demo 
googlesamples-assistant-pushtotalk   
After verifying the working of assistant, close and exit the terminal
HEADLESS AUTOSTART on BOOT SERVICE SETUP

Make the service installer executable
sudo chmod +x /home/pi/GassistPi/scripts/service-installer.sh 
Run the service installer
sudo /home/pi/GassistPi/scripts/service-installer.sh    
Enable the services - Pi3 and Armv7 users, if you need custom wakeword functionality, then enable both the services, else enable just the "gassistpi-ok-ggogle.service" - Pi Zero, Pi A and Pi 1 B+ users, enable snowboy services alone
sudo systemctl enable gassistpi-ok-google.service  
sudo systemctl enable snowboy.service
Start the service - Pi3 and Armv7 users, if you need custom wakeword functionality, then start both the services, else start just the "gassistpi-ok-ggogle.service" - Pi Zero, Pi A and Pi 1 B+ users, start snowboy services alone
sudo systemctl start gassistpi-ok-google.service  
sudo systemctl start snowboy.service   
RESTART and ENJOY

INDICATORS for GOOGLE ASSISTANT'S LISTENING AND SPEAKING EVENTS

Connect LEDs with colours of your choice to GPIO05 for Listening and GPIO06 for Speaking Events.

VOICE CONTROL of GPIOs, SERVO and Pi SHUTDOWN

The default GPIO and shutdown trigger word is trigger. It should be used for controlling the GPIOs, servo and for safe shutdown of Pi.

It has been intentionally included to prevent control actions due to false positive commands. If you wish to change the trigger word, you can replace the 'trigger'in the main.py and assistant.py code with your desired trigger word.

The default keyword for servo motor is servo. For example, the command trigger servo 90 will rotate the servo by 90 degrees.

If you wish to change the keyword, you can replace the 'servo' in the action.py script with your desired keyword for the motor.

For safe shutdown of the pi, command is: trigger shutdown

You can define your own custom actions in the actions.py script.
THE ACTIONS SCRIPT OF THIS PROJECT IS DIFFERENT FROM AIY KIT's SCRIPT, COPY PASTING THE COMMANDS FROM AIY's ACTION SCRIPT WILL NOT WORK HERE. FOR A BETTER UNDERSTANDING OF THE ACTIONS FILE, FOLLOW THE YOUTUBE VIDEO.

Detailed Youtube Video

MUSIC STREAMING from YOUTUBE

Default keyword for playing music from YouTube is Play. For example, Play I got you command will fetch Bebe Rexha's I Got You from YouTube.

Music streaming has been enabled for both OK-Google and Custom hotwords/wakewords.

Due to the Pi Zero's limitations, users are advised to not use the Music streaming fueature. Music streaming will send the CPU usage of Pi Zero into the orbit.

FOR NEOPIXEL INDICAOR

Change the Pin numbers in the given sketch according to your board and upload it.

Follow the circuit diagram given.

Now you have your Google Home Like Indicator
