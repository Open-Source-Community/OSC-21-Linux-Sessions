# Services

Session Moderator : [Mohamed Abdallah](https://github.com/mohamedabdallah20)

A service is a background process that runs without interface by user. This in order to provide even more security, because some of these services are critical for the operation of the operating system.

at sometimes it known as **daemons** and usually these services or daemons names end up with "d". For example, sshd is the name of the service that handles SSH.

to see all the services :

```bash
sudo systemctl list-unit-files --type service --all
```

# Daemons

These are special types of background processes that start at system startup and keep running forever as a service. waiting to be activated by occurrence of a specific event or condition.

# systemd 

Systemd/Init service manger is the mother (parent) of all processes on the system, it’s the first program that is executed when the Linux system boots up; it manages all other processes on the system. It is started by the kernel itself, so in principle it does not have a parent process.

# services status

* **Enabled** : services are currently running. They usually have no problems.
* **Disable** : services are not active but can be activated at any time without a problem.
* **Masked** : 
* **Static**  : services will only be used in case another service or unit needs it.

# Managing services

## Systemctl command

_systemctl_ is the central management tool for controlling the init system / systemd

1. list all services :

```bash
systemctl list-unit-files --type service -all
systemctl --type service -all
```

2. start a services :

```bash
systemctl start <service-name>
```

3. stop a services :

```bash
systemctl stop <service-name>
```

4. restart a service

```bash
systemctl restart <service-name>
```

5. check status of a service :

```bash
systemctl status <service-name>
```

6. enable a service to start with booting

```bash
sudo systemctl enable <service-name>
```

7. disable a service

```bash
sudo systemctl disable <service-name>
```

8. check if service is active or inactive 

```bash
systemctl is-active <service-name>
```

9. check if service is enable or disable

```bash
systemctl is-enabled <service-name>
```

# Create a service

1. ```bash
   cd /etc/systemd/system
   ```
   
2. create a file with extension \(.service\)  \(e.g.  \<my-service.service\>\)

3. include the following 

```bash
[Unit] 
Description=<description about this service> 

[Service] 
User = <user e.g. root> 
WorkingDirectory = <directory_of_script e.g. /root> 
ExecStart = <script which needs to be executed> 
Restart=always

[Install] 
WantedBy=multi-user.target 
```



4. ```bash
   sudo systemctl enable my-service.service
   ```

5. ```bash
   sudo systemctl start my-service.service
   ```
   
   

