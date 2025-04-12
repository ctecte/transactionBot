# Overview
A very simple telegram bot that utilises the telegram API and Python pandas to record transactions into an excel sheet. 

Has simple functions like /month to list all spendings in the current month
/summary to project current month's spendings based on start to current day spendings. Items split by category



# To use
### Create a new variable.env file with the following line
```
bot_token = <your actual bot token>
```
Example
```
bot_token = "abc-dakjdfskladsfjlakdfjafqweqwen123" 
```

### Install the dependencies (if using venv, install these inside the venv)
```
pip install -r /path/to/requirements.txt
```
replace the with the actual path

Example if in the same directory
```
pip install -r requirements.txt
```
### run the bot 
python bot.py

### For practical use, run it on a raspberry pi or orange pi
```
sudo nano /etc/systemd/system/mytelegrambot.service
```
### assuming you have a venv called myenv, use the following systemd service file

```
[Unit]
Description=My Telegram Bot Service
After=network.target

[Service]
# Directly call the python in your venv, passing your bot script
ExecStart=/root/myenv/bin/python /root/transactionBot/bot.py

# (Optional) Have systemd auto-restart on failure
# Remove or comment these lines if you don't want auto-restart
Restart=always
RestartSec=5

# Optional: Clean up lingering processes, prevent zombie/lingering instances of bot
ExecStop=/bin/kill -s TERM $MAINPID

# Run as root (or any other user. Use whoami to get username. Change working directory accordingly)
User=root
WorkingDirectory=/root/transactionBot

# Log to systemd journal
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```
