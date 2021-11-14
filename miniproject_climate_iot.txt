import time

from seeed_dht import DHT

from grove.grove_servo import GroveServo

from grove.grove_light_sensor_v1_2 import GroveLightSensor

from grove.display.jhd1802 import JHD1802

import urllib2


DEBUG = 1

key="JDSASBEVQNTGJCEN"

def main():
    
 
    # Grove - Light Sensor connected to port A0
    lsensor = GroveLightSensor(0)

    # Grove - Temperature&Humidity Sensor connected to port D5
    sensor = DHT('11',16)
    print 'System Ready...'
    URL = 'https://api.thingspeak.com/update?api_key=%s' % key
    print "Wait...."


    while True:
        humi, temp = sensor.read()
        print('temperature {}C, humidity {}%'.format(temp, humi))
        time.sleep(1)
        print('light value {}.'.format(lsensor.light))
        time.sleep(1)
        finalURL = URL +"&field1=%s&field2=%s"%(temp, humi)+"&field3=%s" %(lsensor.light) 
        print finalURL
        s=urllib2.urlopen(finalURL);
 
if __name__ == '__main__':
    main()

