# Notify⁵⁸
Firebase Cloud Messaging server and Android application for sending push notifications from command-line to mobile devices. This is a fork of the [original notify](http://github.com/mashlol/notify) application, modified and customized for personal purposes. I advise not to use this, but instead try the original app which is great and supported.

## Installation
These steps were necessary to implement it on Debian 8.10 Jessie.
### Requirements
 * OpenJDK 1.8 (`sudo apt-get install -t jessie-backports openjdk-8-jdk`)
 * NodeJS v6.11.2 ([nodejs_6.11.2-1nodesource1~jessie1_amd64.deb](https://deb.nodesource.com/node_6.x/pool/main/n/nodejs/nodejs_6.11.2-1nodesource1~jessie1_amd64.deb))
 * NPM v5.8.0 (`sudo npm install -g npm@5.8.0`)

 Optionally to avoid the "sudo-hell" with 'npm' run this below:
```bash
mkdir -p ~/.npm-packages/bin && npm config set prefix ~/.npm-packages && npm list -g --depth=0 && echo -e "\nexport PATH=$HOME/.npm-packages/bin:\$PATH" >> ~/.bashrc && source ~/.bashrc
```

#### Firebase Cloud `(/cloud)`
 1. `npm install -g firebase@4.5.2`
 2. `npm install -g firebase-tools@3.13.1`
 3. `cd functions && npm install`
 4. `firebase login`
 5. `firebase deploy`

#### Notify⁵⁸ Server `(/server)`
 1. `npm install`
 2. `npm start`

#### Android App `(/android)`
	Compiles fine for sure with Android Studio 3.0.1

## Usage
Using notify is simple. When the app installed and launched on the Android device, it will give a unique token. This token is how the device is identified by the server.

**Node JS client** `(clients/node)`:
The notify-client is written with node, so it can be installed with `npm`, then it is available system-wide as command:
```bash
npm install -g
notify -r $TOKEN
notify -i $TITLE -t $MESSAGE
```

**Shell Script** `(clients/sh)`:

```bash
chmod +x notify.sh
./notify.sh -r $TOKEN
./notify.sh -t $MESSAGE
```

**cURL**:
```bash
curl "https://us-central1-notify-58.cloudfunctions.net/sendNotification?to=$TOKEN&title=$TITLE&text=$MESSAGE"
```

**PHP**:

```bash
file_get_contents("https://us-central1-notify-58.cloudfunctions.net/sendNotification?to=$TOKEN&title=$TITLE&text=$MESSAGE")
```

**Pilight Event** `(clients/pilight)`:
It is included in the [pilight-kontrol](https://github.com/gregnau/pilight-kontrol) only.
`IF 1 == 1 THEN pushover TITLE Doorbell rang MESSAGE Doorbell rang TOKEN abcd123abc`


## Example
You will receive a push notification to your phone when the command has completed, regardless of whether or not it was successful:
```bash
someLongRunningCommand && notify
```

## Credits
Most of the credits goes to the original author:
[Kevin Bedi](https://github.com/mashlol)
