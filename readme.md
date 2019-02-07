# OpenTrade is the best opensource cryptocurrency exchange!

Live version: https://tradegloby.pro/


Step-by-step install instructions:

```
apt-get update
apt-get install build-essential libssl-dev curl -y
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh -o install_nvm.sh
bash install_nvm.sh
reboot

nvm install 8.0.0

git clone git@github.com:saydulk/opentrade.git
cd opentrade

npm install 
npm install -g forever
```

## Here is an example of the file ~/opentrade/server/modules/private_constants.js Edit with your configs.
```
'use strict';

exports.recaptcha_priv_key = 'YOUR_GOOGLE_RECAPTCHA_PRIVATE_KEY';
exports.password_private_suffix = 'LONG_RANDOM_STRING1';
exports.SSL_KEY = '../ssl_certificates/privkey.pem'; //change to your ssl certificates private key
exports.SSL_CERT = '../ssl_certificates/fullchain.pem'; //change to your ssl certificates fullchain

exports.walletspassphrase = {
    'MC' : 'LONG_RANDOM_STRING2',
    'BTC' : 'LONG_RANDOM_STRING3',
    'DOGE' : 'LONG_RANDOM_STRING4'
};
```

**After, you can run exchange**

```
cd ~/opentrade/databaseServer
forever start main.js
# if you see NodeJS Forever package minUptime and spinSleepTime warnings then run below command
forever start --minUptime 1000 --spinSleepTime 1000 main.js

cd  ~/opentrade/server
forever start main.js
# if you see NodeJS Forever package minUptime and spinSleepTime warnings then run below command
forever start --minUptime 1000 --spinSleepTime 1000 main.js

```

In your browser address bar, type https://127.0.0.1
You will see OpenTrade.

The first registered user will be exchange administrator. 

# Add trade pairs

For each coin you should create *.conf file
This is common example for "some_coin.conf"

```
rpcuser=long_random_string_one
rpcpassword=long_random_string_two
rpcport=12345
rpcclienttimeout=10
rpcallowip=127.0.0.1
server=1
daemon=1
upnp=0
rpcworkqueue=1000
enableaccounts=1
litemode=1
staking=0
addnode=1.2.3.4
addnode=5.6.7.8

```

Also, you must encrypt your cryptocurrency wallet with this command.

```
./bitcoind encryptwallet random_long_string_SAME_AS_IN_FILE_private_constants.js

```

*If coin is not supported by encryption (like ZerroCash and it forks) the coin can not be added to OpenTrade.*


Add you coin details to OpenTrade

1. Register on exchange. The first registered user will be exchange administrator.
2. Go to "Admin Area" -> "Coins" -> "Add coin"
3. Fill up all fields and click "Confirm"
4. Fill "Minimal confirmations count" and "Minimal balance" and uncheck and check "Coin visible" button
5. Click "Save"
6. Check RPC command for the coin. If it worked then coin was added to the exchange!

All visible coins should be appear in the Wallet. You should create default coin pairs now.

File ~/opentrade/server/constants.js have settings that you can change

https://github.com/3s3s/opentrade/blob/master/server/constants.js

```
exports.NOREPLY_EMAIL = 'no-reply@multicoins.org'; //change no-reply email
exports.SUPPORT_EMAIL = 'ivanivanovkzv@gmail.com'; //change to your valid email for support requests
const DOMAIN = 'localhost'; //Change to your domain name

exports.TRADE_MAIN_COIN = "Marycoin"; //change Marycoin to your main coin pair
exports.TRADE_DEFAULT_PAIR = "Litecoin"; //change Litecoin to your default coin pair
exports.share.TRADE_COMISSION = 0.001; //change trade comission percent
exports.share.DUST_VOLUME = 0.000001; //change minimal order volume

exports.recaptcha_pub_key = "6LeX5SQUAAAAAKTieM68Sz4MECO6kJXsSR7_sGP1"; //change to your recaptcha public key

```

File ~/opentrade/static_pages/chart.html

```
const PORT_SSL = 40443; //change to your ssl port
const MAIN_COIN = 'Marycoin'; //change Marycoin to your main coin pair same as in constants.js
const DEFAULT_PAIR = 'Litecoin'; //change Litecoin to your default coin pair same as in constants.js
      
const TRADE_COMISSION = 0.001;
```

After that, you coins should appear on the main page.

If you need to help setup contact with me Skype: helios-sw or send an email aaccou52@gmail.com

# License

OpenTrade is released under the terms of the MIT license. See LICENSE for more information or see https://opensource.org/licenses/MIT.



