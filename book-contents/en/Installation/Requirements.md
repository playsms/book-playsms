# Requirements

Below requirements, all of them, must be fulfilled before starting the installation.

**Minimum required hardware:**

* For hardware you need only a web server capable hardware

Other hardware you need when you have specific plan:

* GSM modem, single modem, single port, multiple modems or modem pools with multiple ports
	* Required only when you plan to use Kannel, Gammu, Gnokii or smstools gateway plugins
* Internet connection
	* Required only when you plan to use Clickatell, Nexmo, Twilio, Infobip, BulkSMS and Uplink gateway plugins
* LAN
	* Required when you plan to link 2 playSMS on different server in the same network using Uplink gateway plugin
	* Required when you plan to use Kannel and Kannel is on different server in the same network

**Minimum required softwares:**

* Operating System Linux
	* Choose one distro, Ubuntu, Debian, CentOS, or other distro you're familiar with
	* The book will focus on Ubuntu server 15.04
* Web server software, for example Apache2, nginx or lighttpd
	* The book will focus on using Apache2
* Database Server MySQL 5.x.x or latest stable release
* PHP 5.3 at minimum or latest stable release
* PHP MySQL module must be installed and enabled
* PHP CLI must be installed
* PHP gettext extension must be installed and enabled for text translation
	* Please note that on most distro this extension is already compiled and shipped with PHP, so no need to worry about this
* PHP mbstring extension must be installed and enabled for unicode detection
	* Please note that on most distro this extension is already compiled and shipped with PHP, so no need to worry about this
* PHP GD extension must be installed and enabled to draw graphs
* PHP IMAP extension must be installed and enabled to poll Emails from a mailbox
	* This extension will be used by playSMS for Email to SMS plugin
* PHP Mcrypt must be installed to get composer to work properly
* Access to SMTP server for sending Email
	* SMTP server software can be installed locally
	* You can install, configured and start Postfix as your SMTP server
* At least one console browser such as lynx, wget or curl should be installed
* Git must be installed to download Composer packages properly
* Downloaded playSMS package from SF.net or latest source code from Github

**Minimum required server administrator (or developer, or installer):**

* Understand howto make sure required softwares above are installed
* Understand howto configure installed web server
	* The book will focus on server administrator, developer or installer who understand howto configure Apache2
* Understand howto create/drop MySQL database
* Understand howto insert SQL statements into created database
* Basic knowledges to manage Linux
	* Must have the skill to navigate in console mode
