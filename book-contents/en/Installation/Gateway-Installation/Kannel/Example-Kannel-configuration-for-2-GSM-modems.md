# Example Kannel configuration for 2 GSM modems

The scenario is as follow:

* 2 GSM modems with USB connector connected to the server
* Modems used are *wavecom* compatible modems
* 1 modem slotted with SIM card from a carrier with number *+6283874709993*
* The other modem slotted with SIM card also from a carrier with number *+6283875000599*
* playSMS installed, working properly and accessible from `http://localhost/playsms`
* 2 GSM modems configured as 2 SMSCs: `gsm1` and `gsm2`
* Kannel admin and status password is `admpwdnotsafe`
* Kannel sendsms username is `playsms`
* Kannel sendsms password is `sendpwdnotreal`
* Kannel admin port is `13000`
* Kannel send SMS port is `13131`

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

## SMSC gsm1
group = smsc
smsc = at
smsc-id = gsm1
allowed-smsc-id = gsm1
preferred-smsc-id = gsm1
my-number = +6283874709993
#allowed-prefix = "+62;62;0"
unified-prefix = "+62,62,0;+,00"
modemtype = wavecom
device = /dev/ttyUSB0
speed = 115200
validityperiod = 143
sim-buffering = true
max-error-count = 5
log-file = /var/log/kannel/smsc-gsm1.log
log-level = 0

# SMSC gsm2
group = smsc
smsc = at
smsc-id = gsm2
allowed-smsc-id = gsm2
preferred-smsc-id = gsm2
my-number = +6283875000599
#allowed-prefix = "+62;62;0"
unified-prefix = "+62,62,0;+,00"
modemtype = wavecom
device = /dev/ttyUSB1
speed = 115200
validityperiod = 143
sim-buffering = true
max-error-count = 5
log-file = /var/log/kannel/smsc-gsm2.log
log-level = 0

group = modems
id = wavecom
message-storage = SM
need-sleep = true
sendline-sleep = 200
init-string = "AT+CNMI=2,2,0,1,0;+CMEE=1"
#reset-string = "AT+CFUN=1"

group = modems
id = huawei
message-storage = SM
need-sleep = true
sendline-sleep = 200
init-string = "AT+CNMI=2,2,0,1,0;+CMEE=1"
#reset-string = "AT+CFUN=1"

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
