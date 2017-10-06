TELEGRAM.PY

import telepot
import time
bot = telepot.Bot('232181922:AAG5L_UGt9pEvfhL4LqZFTu3Hyjk8srYR-0')
from pprint import pprint
def handle(msg):
        print msg.get('text')
        tmp = msg.get('photo')
        print tmp
        fid = tmp[0].get('file_id')
        fid.decode('utf-8','ignore')
        #print fid
        #print msg.get('file_id')
        bot.download_file(fid, '/root/xyz2.jpg')
bot.message_loop(handle)
print ('Listening ...')

# Keep the program running.
while 1:
    time.sleep(10)

AUDIO_BB2TEL.PY

import time
import Adafruit_BBIO.GPIO as GPIO
import telepot, sys, subprocess

GPIO.setup('P9_15', GPIO.IN)
push =  "P9_15"
while True:
        try:
                if GPIO.input(push):
                        subprocess.call("./record.sh", shell = True)
                        b=telepot.Bot("232181922:AAG5L_UGt9pEvfhL4LqZFTu3Hyjk8srYR-0")
                        b.getMe()
                        df = open('rec.mp3','rb')
                        b.sendAudio(148942492, df)
                        print("Audio sent")
                else:
                        print("no audio")
                        time.sleep(1)
        except KeyboardInterrupt:
                GPIO.cleanup()
                sys.exit(0)

RECORD.SH

#!/bin/bash
rm rec.mp3
arecord -D plughw:1 --duration=10 -f cd -vv rec.mp3
echo "recorded, thank u"
