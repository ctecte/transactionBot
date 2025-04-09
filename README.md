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

# Optional: Clean up lingering processes
ExecStop=/bin/kill -s TERM $MAINPID

# Run as root (since whoami == root)
User=root
WorkingDirectory=/root/transactionBot

# Log to systemd journal
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
