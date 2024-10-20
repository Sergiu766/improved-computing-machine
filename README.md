# improved-computing-machine
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters

# Команда /start
async def start(update: Update, context) -> None:
    await update.message.reply_text('Привет! Я твой бот для приложения Spider.')

# Команда /help
async def help_command(update: Update, context) -> None:
    await update.message.reply_text('Чем я могу помочь? Используй /start, чтобы начать.')

# Ответ на любое сообщение
async def echo(update: Update, context) -> None:
    await update.message.reply_text(f"Ты сказал: {update.message.text}")

# Основная функция для запуска бота
def main():
    # Токен, который ты получил от BotFather
    token = 'ТВОЙ_ТОКЕН_ЗДЕСЬ'

    # Создание приложения
    app = ApplicationBuilder().token(token).build()

    # Регистрация команд и обработчиков
    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("help", help_command))
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, echo))

    # Запуск бота
    app.run_polling()

if __name__ == '__main__':
    main()

