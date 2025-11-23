# hamster_combat_bot.py
import telebot
from telebot import types
import random

# 1️⃣ Bu yerga @BotFather dan olgan tokeningizni qo'ying
TOKEN = 'BU_YERGA_TOKEN_QO‘YASIZ'
bot = telebot.TeleBot(TOKEN)

# 2️⃣ /start buyrug‘i
@bot.message_handler(commands=['start'])
def start(message):
    markup = types.ReplyKeyboardMarkup(row_width=2, resize_keyboard=True)
    btn1 = types.KeyboardButton("jang qil 🐹⚔️")
    btn2 = types.KeyboardButton("statusim 📝")
    markup.add(btn1, btn2)
    bot.send_message(message.chat.id, "salom! hamster jangiga xush kelibsiz! 🐹⚔️", reply_markup=markup)

# 3️⃣ Tugmalarni ishlash
@bot.message_handler(func=lambda message: True)
def action(message):
    if message.text.lower() == "jang qil 🐹⚔️":
        result = random.choice([
            "siz yutdingiz! 🏆",
            "hamster yutdi! 😿",
            "durrang! 🤝"
        ])
        bot.send_message(message.chat.id, result)
    elif message.text.lower() == "statusim 📝":
        bot.send_message(message.chat.id, "hamsteringiz sog‘lom va jangga tayyor! 🐹💪")
    else:
        bot.send_message(message.chat.id, "iltimos, tugmalardan birini tanlang!")

# 4️⃣ Botni ishga tushurish
bot.polling()
