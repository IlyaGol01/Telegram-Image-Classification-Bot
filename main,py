import telebot
from config import api
from logic_ai import get_class

bot = telebot.TeleBot(api)

@bot.message_handler(content_types=['photo'])
def get_photo(message):
    file_info = bot.get_file(message.photo[-1].file_id)
    file_name = file_info.file_path.split('/')[-1]
    downloaded_file = bot.download_file(file_info.file_path)
    with open(file_name, 'wb') as new_file:
        new_file.write(downloaded_file)
    class_name, score = get_class(file_name)
    bot.reply_to(message, class_name)
    if class_name == "Голубь":
        bot.reply_to(message, "Это голубь, тест")
    if class_name == "Синица":
        bot.reply_to(message, "Это синица, тест")
    else:
        bot.reply_to(message, "Произошла ошибка")

bot.polling()
