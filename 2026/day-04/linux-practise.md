# Day 04 – Linux Practice

-----------------------------------------------------------------

## Process commands:

### top : Provides a real-time, dynamic view of running processes.

output:

<img width="468" height="144" alt="top" src="https://github.com/user-attachments/assets/2bb91bba-a309-455a-a896-c70da846efe3" />

### ps aux : Displays a static snapshot of all running processes in the system

output:

<img width="468" height="124" alt="ps aux" src="https://github.com/user-attachments/assets/c0ecc7e0-943d-4d0d-9f27-0d55f5e92202" />

--------------------------------------------------------------------------------------

## Service commands

### Systemctl status sshd : To check status of the service

output:

<img width="468" height="157" alt="service status" src="https://github.com/user-attachments/assets/6459fcdd-2e27-440d-9b0b-8c71cf1fc8c0" />

### systemctl list-units --type=service:  displays all currently loaded and active systemd service units.

output: 

<img width="468" height="157" alt="service status" src="https://github.com/user-attachments/assets/0fc9e9fd-fa0e-4f65-bf40-24cf9311c22c" />

-----------------------------------------------------------------------------------------------------

## Log commands

### Journalctl -u ssh :  a powerful Linux utility for querying and displaying log messages from the system journal

output: 

<img width="468" height="122" alt="journatlctl" src="https://github.com/user-attachments/assets/eb0d9554-f3ba-441b-8dc3-afd79c6ccfad" />

### Journalctl -u ssh -n 20 : display recent logs of ssh which will be helpful for troubleshooting

output:

<img width="468" height="94" alt="latest logs" src="https://github.com/user-attachments/assets/0d8b1ca1-9976-418d-b0cd-656a152dd4a8" />

-----------------------------------------------------------------------------------------------------------

## Mini troubleshooting

### Scenario ssh not working

# 1.Check if service is running using systemctl status ssh

<img width="468" height="137" alt="service status1" src="https://github.com/user-attachments/assets/44542416-10d4-449a-9d71-a3d5bb19559d" />

# 2.Service is inactive start the service using systemctl start ssh now the status shows it is active

<img width="468" height="155" alt="active service" src="https://github.com/user-attachments/assets/fa417c09-7e90-4afd-91c5-ecc5f33566ff" />

# 3.Now to check what was the cause use log commands
Journalctl -u ssh -n 20

<img width="468" height="144" alt="check logs" src="https://github.com/user-attachments/assets/21aa220c-6472-4526-9053-31f13c86708f" />

## ✅ What I Learned

- Learned how to check running processes
- Learned how to inspect services
- Learned how to check logs




