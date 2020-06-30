# Octowait

**A raspberryPi-powered eInk delay time indicator to minimise cost on Octopus Agile tariffs**

## 1. Assemble the parts

- [Inky pHat](https://amzn.to/3gm150T) £20
- [Pi ZeroWH (with soldered headers)](https://amzn.to/2BN2oGY) £30
- [16GB MicroSD](https://amzn.to/3i6PXX8) £5

## 2. Install requirements

- Follow standard instructions to get [Raspberry Pi OS](https://www.raspberrypi.org/downloads/) installed.
- Follow standard instructions to enable wifi: [Setting up a Raspberry Pi headless](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
- Follow standard instructions to enable ssh: [SSH (Secure Shell)](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md)
- ssh in to your pi
- install the `inky` code (say no to the additional code): `curl https://get.pimoroni.com/inky | bash`
- clone this repo into your home folder: `git clone https://github.com/simonhearne/octowait.git`
- install pip: `apt-get install python3-pip`
- change dir to the project: `cd octowait`
- install python dependencies: `pip install -r requirements.txt`

## 3. Test run

For convenience, you can make the python file executable: `chmod +x run.py`.
Run the script to see if there are any errors: `./run.py`

You can edit the script to change variables such as how long the task is (e.g. a wash might be three hours), what tariff you are on and whether to flip the image.
Feel free to play around with the script to change fonts, graph etc!

## 4. Schedule to run every 15 minutes

Open crontab (you may need to choose your preferred editor): `crontab -e`
Add the following to the end of the file:

`*/15 * * * * cd /home/pi/octowait && ./run.py >/dev/null 2>&1`

## 5. Profit!

Check the screen when you go to set your dishwasher, washing machine, tumble dryer, slow cooker etc.
Set the delay that is recommended, see your energy bills plummet!

If you are not yet on Octopus Agile - use this link to get £50 credit when you switch (plus you get free smart meters & in-home display!)
<https://share.octopus.energy/jolly-louse-561>

## 6. Save power

If you are running the Pi off a battery, or are just energy conscious, you can run the following commands:

- Disable HDMI output: `sudo /opt/vc/bin/tvservice -o`
- Disable Bluetooth: `echo 'dtoverlay=pi3-disable-bt' >> /boot/config.txt`
- Disable LED: `echo 'dtparam=act_led_trigger=none' >> /boot/config.txt`

You'll need to reboot your Pi for these to have an effect: `sudo reboot now`
