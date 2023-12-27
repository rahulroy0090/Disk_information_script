## Script for sent alert of multiple server


```
cat phone3.py 
import time
import psutil
from email.mime.text import MIMEText
import smtplib
import paramiko

# Function to check disk usage on a remote server via SSH
def check_remote_disk_usage(hostname, username, password):
    try:
        # Establish SSH connection
        ssh_client = paramiko.SSHClient()
        ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
        ssh_client.connect(hostname, username=username, password=password)

        # Get disk usage
        stdin, stdout, stderr = ssh_client.exec_command("df -h /")
        output = stdout.read().decode("utf-8")
        
        # Extract disk usage percentage
        disk_usage_percent = int(output.split("\n")[1].split()[4].replace("%", ""))
        
        return disk_usage_percent

    except Exception as e:
        print(f"Error checking disk usage on {hostname}: {e}")
        return None

    finally:
        ssh_client.close()

# Function to send disk alert email
def send_disk_alert_email(server, disk_usage_percent):
    # Your email alert configuration here
    sender_email = 'royraj4998@gmail.com'
    sender_password = 'qnmw ugdn wzjv oyse'
    receiver_email = 'royraj4998@gmail.com' 
    smtp_server = 'smtp.gmail.com'
    smtp_port = 587

    # Compose email message
    subject = f'Disk Usage Alert on {server}!'
    body = f'Disk usage on {server} is {disk_usage_percent}%. Please take action!\n\n{get_system_info()}'

    msg = MIMEText(body)
    msg['Subject'] = subject
    msg['From'] = sender_email
    msg['To'] = receiver_email

    # Connect to SMTP server and send email
    with smtplib.SMTP(smtp_server, smtp_port) as server:
        server.starttls()
        server.login(sender_email, sender_password)
        server.sendmail(sender_email, receiver_email, msg.as_string())

# Function to get local system information
def get_system_info():
    ram = psutil.virtual_memory()
    disk = psutil.disk_usage('/')
    
    system_info = f"Local System Information:\n" \
                  f"  RAM Information:\n" \
                  f"    Total RAM: {ram.total / (1024 ** 3):.2f} GB\n" \
                  f"    Used RAM: {ram.used / (1024 ** 3):.2f} GB\n" \
                  f"    Free RAM: {ram.available / (1024 ** 3):.2f} GB\n" \
                  f"  Disk Information:\n" \
                  f"    Total Disk Space: {disk.total / (1024 ** 3):.2f} GB\n" \
                  f"    Used Disk Space: {disk.used / (1024 ** 3):.2f} GB\n" \
                  f"    Free Disk Space: {disk.free / (1024 ** 3):.2f} GB\n" \
                  f"    Disk Usage Percentage: {disk.percent}%"

    return system_info

if __name__ == "__main__":
    # Configuration for remote servers
    server1 = {'hostname': '192.168.122.1', 'username': 'rahul', 'password': '123'}
    server2 = {'hostname': '192.168.122.65', 'username': 'rahul', 'password': '123'}

    try:
        while True:
            # Check disk usage on remote servers
            disk_usage_server1 = check_remote_disk_usage(server1['hostname'], server1['username'], server1['password'])
            disk_usage_server2 = check_remote_disk_usage(server2['hostname'], server2['username'], server2['password'])

            # Send alerts if disk usage is 96% or higher on any server
            if disk_usage_server1 is not None and disk_usage_server1 >= 26:
                send_disk_alert_email(server='Server 1', disk_usage_percent=disk_usage_server1)

            if disk_usage_server2 is not None and disk_usage_server2 >= 96:
                send_disk_alert_email(server='Server 2', disk_usage_percent=disk_usage_server2)

            # Adjust the sleep time to check more frequently (e.g., every 1 minute)
            time.sleep(60)

    except KeyboardInterrupt:
        print("\nScript interrupted. Exiting gracefully.")

```





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
