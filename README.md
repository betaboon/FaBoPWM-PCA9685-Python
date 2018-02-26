# FaBoPWM-PCA9685-Python
#### install
```
git clone https://github.com/FaBoPlatform/FaBoPWM-PCA9685-Python
pip install FaBoPWM-PCA9685-Python/
```

#### uninstall
```
pip uninstall Fabo_PCA9685
```

#### usage
```python
# coding: utf-8
import Fabo_PCA9685
import time
import pkg_resources
SMBUS='smbus'
for dist in pkg_resources.working_set:
    #print(dist.project_name, dist.version)
    if dist.project_name == 'smbus':
        break
    if dist.project_name == 'smbus2':
        SMBUS='smbus2'
        break
if SMBUS == 'smbus':
    import smbus
elif SMBUS == 'smbus2':
    import smbus2 as smbus

# init
BUSNUM=1
SERVO_HZ=50
INITIAL_VALUE=300
bus = smbus.SMBus(BUSNUM)
PCA9685 = Fabo_PCA9685.PCA9685(bus,INITIAL_VALUE)
PCA9685.set_hz(SERVO_HZ)

# set value
value = 330
channel = 0 # PWM0番目のピンのサーボ
PCA9685.set_channel_value(channel,value)

# get value(Get chip register's value. This value may not be equal to the actual position.)
value = PCA9685.get_channel_value(channel)
print(value)

time.sleep(1)

value = 300
channel = 0 # PWM0番目のピンのサーボ
PCA9685.set_channel_value(channel,value)

# get value(Get chip register's value. This value may not be equal to the actual position.)
value = PCA9685.get_channel_value(channel)
print(value)
```
