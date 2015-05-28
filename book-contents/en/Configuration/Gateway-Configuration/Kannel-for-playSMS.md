# Kannel for playSMS


## Intro

In this section we will use example Kannel installation based on [Kannel installation on Ubuntu](../../Installation/Gateway-Installation/Kannel/Kannel-installation-on-Ubuntu.md) section.
And the case study is based on [Example Kannel configuration for 2 GSM modems](../../Installation/Gateway-Installation/Kannel/Example-Kannel-configuration-for-2-GSM-modems.md) section.

Here are informations related to Kannel from the case study:

* playSMS installed, working properly and accessible from `http://localhost/playsms`
* 2 GSM modems configured as 2 SMSCs: `gsm1` and `gsm2`
* Kannel send SMS username is `playsms`
* Kannel send SMS password is `sendpwdnotreal`
* Kannel send SMS port is `13131`
* Kannel admin and status password is `admpwdnotsafe`
* Kannel admin port is `13000`


## Configure gateway

1. Login as admin account to playSMS at `http://localhost/playsms`

2. Go to menu `Settings -> Manage gateway and SMSC`

3. On tab `Gateways` look for `kannel` with description `Gateway Kannel` and click the `Edit` button on the right side (the grind icon)

4. Now you are in `Manage kannel` page, fill in options according to your setups, in this section they are according to the case study

   * Fill option `Username` with Kannel send SMS username `playsms`
   * Fill option `Password` with Kannel send SMS password `sendpwdnotreal`
   * Usually you need to select `Yes` to option `Incoming SMS time is in local time`
   * For now leave the option `Bearerbox hostname or IP` and `Send SMS hostname or IP` to `localhost`
     * This is because in the case study playSMS URL and Kannel are both accessible from hostname `localhost`
   * Fill option `Send SMS port` with Kannel send SMS port `13131`
   * Usually you want to check all the `Delivery Report` checkboxes
   * Fill option `playSMS web URL` with the actual URL of installed playSMS, in this case study its accessible from `http://localhost/playsms`
   * Fill option `Kannel admin host` with `localhost`
   * Fill option `Kannel admin port` with `13000`
   * Fill option `Kannel admin password` with `admpwdnotsafe`
   * Click the `Save` button below the page to save the gateway configuration

5. If all good you should see some information in `Kannel status` textarea

   * You will see nothing if Kannel is not running or not configured properly
   * You will see access denied information if the Kannel admin host, port or password does not match


## Configure SMSC

1. Login as admin account to playSMS at `http://localhost/playsms`

2. Go to menu `Settings -> Manage gateway and SMSC`

3. On tab `Gateways` look for `kannel` with description `Gateway Kannel` and click the `Add` button on the right side (the plus sign icon)

4. Now you are in `Add SMSC` page, fill in options according to your `kannel.conf`, in this section they are according to the case study

   * Fill option `SMSC name` with any 1 word text, but recommended to use the same name as configured in `kannel.conf`, so fill it with `gsm1`
   * Fill option `Additional URL parameter` with `smsc=gsm1`
   * Click the `Save` button below the page to save SMSC configuration
   * Click the `Back` button to go back to `Manage gateway and SMSC` page
   * Add 1 more SMSC, next is to add `gsm2` since we have 2 SMSCs, `gsm1` and `gsm2`, configured in `kannel.conf`

5. Go back to `Manage gateway and SMSC` page and then click the `SMSCs` tab

   * You should see that you have added `gsm1` and `gsm2`


## Next

1. You may go to `Settings -> Main configuration` and set `Default SMSC`

2. You may then go to `Settings -> Route outgoing SMS` and set route to your SMSCs based on prefix

My recommendation is to set `Default SMSC` to `blocked` and route outgoing SMS based on prefix to specific SMSC.
You can also use same prefix for multiple SMSCs, and playSMS will choose randomly which SMSC that will be used to deliver SMS when prefix matched.
