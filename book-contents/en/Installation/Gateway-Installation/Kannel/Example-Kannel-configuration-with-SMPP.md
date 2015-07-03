# Example Kannel configuration with SMPP

The scenario is as follow:

* playSMS installed, working properly and accessible from `http://localhost/playsms`
* 2 SMPP connection details from 2 different providers
* 2 SMPP connection configured as 2 SMSCs: `smpp1` and `smpp2`
* Kannel send SMS username is `playsms`
* Kannel send SMS password is `sendpwdnotreal`
* Kannel send SMS port is `13131`
* Kannel admin and status password is `admpwdnotsafe`
* Kannel admin port is `13000`

Below is the working `kannel.conf` to match above scenario:

```
# CORE
group = core
admin-port = 13000
admin-password = admpwdnotsafe
status-password = admpwdnotsafe
log-file = /var/log/kannel/kannel.log
log-level = 0
access-log = /var/log/kannel/access.log
smsbox-port = 13001
store-type = spool
store-location = /var/spool/kannel/store
smsbox-max-pending = 100

# SMSBOX
group = smsbox
bearerbox-host = localhost
bearerbox-port = 13001
sendsms-port = 13131
sendsms-chars = "0123456789+ "
log-file = /var/log/kannel/smsbox.log
log-level = 0
access-log = /var/log/kannel/access.log
mo-recode = true

# SMSC smpp1
smsc = smpp
smsc-id = smpp1
allowed-smsc-id = smpp1
preferred-smsc-id = smpp1
host = SMPP1_SERVER_ADDRESS_CHANGE_THIS
port = SMPP1_SERVER_PORT_NUMBER_CHANGE_THIS
transceiver-mode = yes
smsc-username = SMPP1_USERNAME_CHANGE_THIS
smsc-password = SMPP1_PASSWORD_CHANGE_THIS
system-type = "VMA"
log-file = /var/log/kannel/smsc-smpp1.log
log-level = 0

# SMSC smpp2
smsc = smpp
smsc-id = smpp2
allowed-smsc-id = smpp2
preferred-smsc-id = smpp2
host = SMPP2_SERVER_ADDRESS_CHANGE_THIS
port = SMPP2_SERVER_TX_PORT_NUMBER_CHANGE_THIS
receive-port = SMPP2_SERVER_RX_PORT_NUMBER_CHANGE_THIS
transceiver-mode = no
smsc-username = SMPP2_USERNAME_CHANGE_THIS
smsc-password = SMPP2_PASSWORD_CHANGE_THIS
system-type = ""
log-file = /var/log/kannel/smsc-smpp2.log
log-level = 0

# SENDSMS-USER
group = sendsms-user
default-smsc = none
username = playsms
password = sendpwdnotreal
max-messages = 6
concatenation = true

# SMS SERVICE
group = sms-service
keyword = default
omit-empty = true
max-messages = 0
get-url = "http://localhost/playsms/index.php?app=call&cat=gateway&plugin=kannel&access=geturl&t=%t&q=%q&a=%a&Q=%Q&smsc=%i"
```
