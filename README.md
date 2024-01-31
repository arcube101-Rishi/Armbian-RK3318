# Armbian-RK3318
I wanted to crawl and scrape some sites repeatedly and did not want my main PC running 24x7.
There are plenty of cheap android tv boxes available on AliExpress and consume very little power, approx 5 - 7w, so I bought some for US$22 each and converted them to Armbian.
In my opinion these boxes have enough power to run python based scrapy as most of the time program/scraper is waiting for net IO, a quick search on AliExpress produced these 2 –

Link1 $20.50
Link2 $37

Spec to look for:
Rk3318 based SOC   <<<< this is important*
Any android version (it would be removed)
Mini wireless keyboard (they work on 2.4ghz via a usb dongle)

*There are many types of android boxes but in my opinion RK3318 (or RK3328) soc based are best supported due to the active involvement of developer jock and fabiobassa, some multi-billion-dollar corporations should take cues from them on how to support.

First:
- You need mini keyboard connected for initial setup
- HDMI cable & TV/Monitor for initial setup
- WiFi may(?) not work so you need an ETHERNET cable
- SD Card (at-least 8GB)

Process:
Installing Armbian
      There are very good detailed instructions on Armbian forum (Link) (READ CAREFULLY)
      burn it to eMMC for best performance  (READ TWICE)

1. Download multitool
2. Download Balena Etcher
3. Download Image for RK3318

- Use balena etcher to write/burn multitool on a SD Card (~8GB)
- Remove SD card from windows and then insert it back
- Windows Explorer should open else manually browse to SD card folders
- Place the “Image for RK3318” in the “images” folder of the SD card
- Insert SD card into tv box and reboot, by removing and reinserting power after 30 seconds
- Choose Burn Image to flash when it appears
 

IF ALL WENT WELL:
After it reboots you should see a prompt to create an account and change password for root
Create an account for you, it would be sudo activated i.e. similar permissions as admin/root

Additional Packages:
You will need to install additional packages for scrapy and update any old packages so you need to type below commands
sudo apt --yes update
sudo apt upgrade
sudo apt install python3-pip
sudo apt install python3.11-venv
 

Optionally I also installed
sudo apt install vim
sudo apt install net-tools (ifconfig is missing)
sudo apt install armbian-config
Then make a directory where you want to install scrapy, I called mine as “StockScraper”
mkdir -p StockScraper
cd StockScraper
python3 -m venv .venv
source .venv/bin/activate
pip install scrapy
pip install scrapy-rotating-proxies (optional)
pip install scrapy-user-agents (optional)

Creating 1st scrapy project
scrapy startproject scraper /home/<your_account>/StockScraper
Find out your network interface and IP Address

ifconfig
It should print out something like below, you need to note down IP Address
![image](https://github.com/arcube101-Rishi/Armbian-RK3318/assets/97570658/cb254d73-5c33-4f43-9d18-1a44baf825a1)

At this point everything is setup and you can remove HDMI if you want to and do a ssh into box from your PC (windows / linux)

Open a windows command prompt and type
ssh 192.168.50.47


There are many more changes which can be done to optimize this setup:
