
## Sent the alert 96% disk used.



```
cat phone2.py 
import time
import psutil
from email.mime.text import MIMEText
import smtplib

def get_system_info():
    ram = psutil.virtual_memory()
    disk = psutil.disk_usage('/')
    
    system_info = f"RAM Information:\n" \
                  f"  Total RAM: {ram.total / (1024 ** 3):.2f} GB\n" \
                  f"  Used RAM: {ram.used / (1024 ** 3):.2f} GB\n" \
                  f"  Free RAM: {ram.available / (1024 ** 3):.2f} GB\n\n" \
                  f"Disk Information:\n" \
                  f"  Total Disk Space: {disk.total / (1024 ** 3):.2f} GB\n" \
                  f"  Used Disk Space: {disk.used / (1024 ** 3):.2f} GB\n" \
                  f"  Free Disk Space: {disk.free / (1024 ** 3):.2f} GB\n" \
                  f"  Disk Usage Percentage: {disk.percent}%"

    return system_info

def send_disk_alert_email():
    # Your email alert configuration here
    sender_email = 'royraj4998@gmail.com'
    sender_password = 'qnmw ugdn wzjv oyse'
    receiver_email = 'royraj4998@gmail.com' 
    smtp_server = 'smtp.gmail.com'
    smtp_port = 587

    # Check disk usage
    disk = psutil.disk_usage('/')
    if disk.percent >= 25:
        # Compose email message with detailed system information
        subject = 'Disk Usage Alert!'
        body = f'Disk usage is 96% or higher. Please take action!\n\n{get_system_info()}'

        msg = MIMEText(body)
        msg['Subject'] = subject
        msg['From'] = sender_email
        msg['To'] = receiver_email

        # Connect to SMTP server and send email
        with smtplib.SMTP(smtp_server, smtp_port) as server:
            server.starttls()
            server.login(sender_email, sender_password)
            server.sendmail(sender_email, receiver_email, msg.as_string())

if __name__ == "__main__":
    try:
        while True:
            send_disk_alert_email()  # Call the email function directly
            # Adjust the sleep time to check more frequently (e.g., every 1 minute)
            time.sleep(60)
    except KeyboardInterrupt:
        print("\nScript interrupted. Exiting gracefully.")


```




```
import time
import psutil
from email.mime.text import MIMEText
import smtplib

def check_disk_usage():
    disk = psutil.disk_usage('/')
    if disk.percent >= 30:
        send_disk_alert_email()

def send_disk_alert_email():
    # Your email alert configuration here
    sender_email = 'royraj4998@gmail.com'
    sender_password = 'qnmw ugdn wzjv oyse'
    receiver_email = 'royraj4998@gmail.com' 
    smtp_server = 'smtp.gmail.com'
    smtp_port = 587

    # Compose email message
    subject = 'Disk Usage Alert!'
    body = 'Disk usage is 96% or higher. Please take action!'

    msg = MIMEText(body)
    msg['Subject'] = subject
    msg['From'] = sender_email
    msg['To'] = receiver_email

    # Connect to SMTP server and send email
    with smtplib.SMTP(smtp_server, smtp_port) as server:
        server.starttls()
        server.login(sender_email, sender_password)
        server.sendmail(sender_email, receiver_email, msg.as_string())

if __name__ == "__main__":
    try:
        while True:
            check_disk_usage()
            # Adjust the sleep time to check more frequently (e.g., every 1 minute)
            time.sleep(60)
    except KeyboardInterrupt:
        print("\nScript interrupted. Exiting gracefully.")


```






```
# Update and install python3:
sudo apt-get update
sudo apt-get install python3

# Install Required Packages:
sudo apt-get install python3-pip

# Install the required Python modules
pip3 install smtplib psutil


```


```
import smtplib
from email.mime.text import MIMEText
import psutil

def get_ram_info():
    ram = psutil.virtual_memory()
    ram_info = f"Total RAM: {ram.total / (1024 ** 3):.2f} GB\n" \
                f"Used RAM: {ram.used / (1024 ** 3):.2f} GB\n" \
                f"Free RAM: {ram.available / (1024 ** 3):.2f} GB"
    return ram_info

def get_disk_info():
    disk = psutil.disk_usage('/')
    disk_info = f"Total Disk Space: {disk.total / (1024 ** 3):.2f} GB\n" \
                 f"Used Disk Space: {disk.used / (1024 ** 3):.2f} GB\n" \
                 f"Free Disk Space: {disk.free / (1024 ** 3):.2f} GB\n" \
                 f"Disk Usage Percentage: {disk.percent}%"
    return disk_info

def send_system_info_email():
    # Email configuration
    sender_email = 'royraj4998@gmail.com'
    sender_password = 'qnmw ugdn wzjv oyse'
    receiver_emails = ['royraj4998@gmail.com', 'rockyrajj45@gmail.com', 'rahul_kumar@fosteringlinux.com', 'devendra.sharma@fosteringlinux.com', 'mansi.rastogi@fosteringlinux.com']
    smtp_server = 'smtp.gmail.com'
    smtp_port = 587

    # Compose email message with system information
    subject = 'System Information'
    body = f"RAM Information:\n{get_ram_info()}\n\nDisk Information:\n{get_disk_info()}"
    msg = MIMEText(body)
    msg['Subject'] = subject
    msg['From'] = sender_email
    msg['To'] = ', '.join(receiver_emails)

    # Connect to SMTP server and send email
    with smtplib.SMTP(smtp_server, smtp_port) as server:
        server.starttls()
        server.login(sender_email, sender_password)
        server.sendmail(sender_email, receiver_emails, msg.as_string())

if __name__ == "__main__":
    send_system_info_email()

```

```
# Run this script:
python3 system.py

```
