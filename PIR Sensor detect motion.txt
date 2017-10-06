import Adafruit_BBIO.GPIO as GPIO
import time
import sys
import subprocess
import telepot
GPIO.setup('P9_15',GPIO.IN)
GPIO.setup('P9_16',GPIO.IN)
while True:
        try:
                if GPIO.input('P9_15'):
                        print("motion detected")
                        subprocess.call("./fs.sh", shell=True)
                        b=telepot.Bot('232181922:AAG5L_UGt9pEvfhL4LqZFTu3Hyjk8srYR-0')
                        b.getMe()
                        df = open('photo2.jpg','rb')
                        b.sendPhoto(148942492,df)
                else:
                        print("Motion not detected")
                if GPIO.input('P9_16')

                time.sleep(1)
        except KeyboardInterrupt:
                GPIO.cleanup()
                sys.exit()
