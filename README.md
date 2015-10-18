spoofident
==========

Spoof ident daemon. Nimble Pythonic spoof identd. Please note that this is not a "real" identd -- it will not return correct information for which user is using which port. Instead, it will reply with a username and OS of your choice to all requests.

Installation
====
1. git clone the repo  
	`git clone git@github.com:flotwig/spoofident.git`  
	`cd ./spoofident/`
2. Copy the config.json.example file to config.json and fill out the settings. Here follows an explanation for the various settings:  
	* **listeners**: An array of two-value arrays -- host/port pairs which spoofident will listen on. By default, it is set to ["::",113]; that is, the identd port on all IPv4 and IPv6 interfaces. You may need to set it to ["0.0.0.0",113] if your system lacks IPv6 support.
	* **setuid**: Very important. This is the user ID which spoofident will drop down to. Because ident runs on a port <1000, it requires root privileges to bind to that port. Even though spoofident is a very secure daemon, it's poor practice to run any server as root, so spoofident will drop to this uid immediately after binding to the listeners specified. Please note that this is a uid, not a username - it is a numerical ID for a user on your system. By default it is 65534, the standard ID for "nobody" on Linux.
	* **setgid**: Same as **setuid** but for group ID. By default 65534 for nogroup.
3. Run spoofident.py as root to start the daemon.  
	`sudo python spoofident.py &`
4. Add `python /path/to/spoofident.py` to /etc/rc.local to start spoofident on system startup.
