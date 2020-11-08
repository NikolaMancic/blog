# Connecting via Cockpit

## What is Cockpit

## Installation

``` sh
# Install cockpit
apt install cockpit

# Start the cockpit service
systemctl start cockpit

# Check the status of the cockpit service
systemctl status cockpit
```

If started successfully the output of `systemctl status` should contain something like:

``` sh
Active: active (running) since ...
```

## Connecting to Cockpit

Try connecting to cockpit on your host operating system.

Open a web browser and either type a DNS name or IP address followed by cockpit's default port number 9090

Examples:

* `192.168.1.100:9090`
* `pi-red:9090`

You should see the login page

![cockpit login](/posts/cockpit/images/cockpit-login.png)

Enter any valid credentials for the system you're accessing. Once logged in you should see a dashboard

![cockpit dashboard](/posts/cockpit/images/cockpit-dashboard.png)

Cockpit gives you an overview of several aspects of your system. Feel free to browse around and learn more [here](https://cockpit-project.org/)
