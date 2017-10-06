SENDP.PY

from twx.botapi import TelegramBot, ReplyKeyboardMarkup

f =  open('photo2.jpg','r+')
jpgdata = f.read()

bot = TelegramBot('232181922:AAG5L_UGt9pEvfhL4LqZFTu3Hyjk8srYR-0')
bot.update_bot_info().wait()
user_id = int(148942492)
bot.send_photo(user_id,'/home/debian/photo2.jpg')

f.close()
