import os, datetime, time
from OmegaExpansion import oledExp
from subprocess import Popen, PIPE

# find current time
currentTime = datetime.datetime.now()

# measure and format battery voltage
program = Popen("power-dock2", stdin=PIPE, stdout=PIPE, stderr=PIPE)
output, err  = program.communicate()
battery_text = "Battery(V): " +  output[-7:]

# converting a string value of the battery to a float value
Vcurrent = float(output[-7:-2])

# math function to determine the battery percentage
Vmax = 4.2
Vmin = 3.5
battery_percentage = ((Vcurrent-Vmin)/(Vmax-Vmin))*100
battery_percentage =int(battery_percentage)


# initialize the oled
status = oledExp.driverInit()

# write content to oled
oledExp.write("Current date and time ")
oledExp.write(currentTime.strftime("%Y-%m-%d %H:%M:%S"))

oledExp.setCursor(3, 0)
oledExp.write(battery_text)

oledExp.setCursor(5, 0)
oledExp.write('Battery(%): ' + str(battery_percentage) + '%')
