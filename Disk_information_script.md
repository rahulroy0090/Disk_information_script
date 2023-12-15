

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
