# oled-display-battery
A program to display the battery level and current time on the OLED Display

# Components needed
You need the following list of items:
*Power Dock 2
*OLED Expansion
*Omega2/2+
*3.7 LiPo Battery

# Purpose
Retreives battery charge and displays on the OLED screen along with the current date and time

# Installation
Once you have compined all items together, you need to run following commands:
```
opkg update
opkg install python-light pyOledExp power-dock2
```
Now copy the python program `oled-display-battery.py` to your root directory. This project was meant to start on boot and update the information every minute. To do so, we need to initialize the cron settings.
Copy a file called oled_battery_display_cron.sh into your root directory, make it executable by issuing `chmod +x /root/oled_battery_display_cron.sh` and start your cron job by issuing `crontab -e` and populate it with the following text
```
#
*/1 * * * * /root/oled_battery_display_cron.sh
#
```
Save your changes and restart the cron daemon with the following command `/etc/init.d/cron restart

And you are all set! You will see updated info on your OLED screen every minute and the program itself will start on the boot.
