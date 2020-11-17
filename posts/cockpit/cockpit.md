# Connecting via Cockpit

## What is Cockpit

Cockpit is a remote administration tool that lets you monitor resource usage, run system tasks and connect via SSH in a convenient web based GUI.

## Installation

``` sh
# Install cockpit
apt install cockpit

# Check if the service is running
service cockpit status

# Run the service if it's not running already
service cockpit start
```

## Connecting to Cockpit

Try connecting to cockpit on your local computer.

Open a web browser and either type a DNS name or IP address followed by cockpit's default port number 9090

Examples:

* `192.168.1.100:9090`
* `pi-red:9090`

You should see the login page

![cockpit login](/posts/cockpit/images/cockpit-login.png)

Enter any valid credentials for the system you're accessing. Once logged in you should see a dashboard

![cockpit dashboard](/posts/cockpit/images/cockpit-dashboard.png)

Cockpit gives you an overview of several aspects of your system. Feel free to browse around and learn more [here](https://cockpit-project.org/)
