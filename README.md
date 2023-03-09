<h1 align="center"> Q Blockchain </h1>

## System requirements:

```
4 vCPUs
8GB RAM
250GB SSD
```

## We set the variables:

* Set a password
```
PASSWORD=Set Password
```
* Edit the PASSWORD
```
echo "export PASSWORD=PASSWORD" $HOME/.bash_profile
source $HOME/.bash_profile
```

## Make the updates one by one

* Press Y and ENTER in Y/N questions in some updates
```
sudo apt update
```
```
sudo apt upgrade
```
```
apt install docker-compose
```
```
apt install npm
```
```
apt install screen
```
```
sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
```

## We create binary and pwd:

* Enter commands one by one
* Edit the password part

```
git clone https://gitlab.com/q-dev/testnet-public-tools.git
cd testnet-public-tools/testnet-validator/
mkdir keystore
cd keystore/
echo "PASSWORD" >> pwd.txt
```

## Let's create a wallet and save the information:

* Let's get a token for our 0x wallet: [Faucet](https://faucet.qtestnet.org/)

```
cd..
docker run --entrypoint="" --rm -v $PWD:/data -it qblockchain/q-client:testnet geth account new --datadir=/data --password=/data/keystore/pwd.txt
```

## We will edit the configuration file:

* Let's enter the non-0x key in the address section
* Exit with CTRL X Y ENTER

```
cp .env.example .env
nano .env
```

![image](https://user-images.githubusercontent.com/101149671/206860212-79018b15-b65d-4291-8054-8785b0078153.png)

## Same action:

* Edit the address and password.
* address 0xless address, we have specified above in the password.
* Exit with CTRL X Y ENTER
```
nanoconfig.json
```
![image](https://user-images.githubusercontent.com/101149671/206860284-853e9661-3f8a-4d0d-b343-9adf93ff62ea.png)

## Let's stake our tokens

* If this command does not work, you have missing the configuration files (`.env` and `config.json`) above.

```
docker run --rm -v $PWD:/data -v $PWD/config.json:/build/config.json qblockchain/js-interface:testnet validators.js
```

## Now we create the private key:
```
CD
cd testnet-public-tools
chmod +x run-js-tools-in-docker.sh
./run-js-tools-in-docker.sh
npm install
```
* Don't forget to edit 0XLICUZDAN and PASSWORD here!
* At the end of this process, a folder named PK will be created.
* Exit NPM with CTRL A D.
```
chmod +x extract-geth-private-key.js
node extract-geth-private-key 0XLİCÜZDAN ../testnet-validator/ PASSWORD
```

## Connect to your server with WinSCP or Mobaxterm:

* file will be in `/root/testnet-public-tools/js-tools`
* When we click inside it will give us a key

![image](https://user-images.githubusercontent.com/101149671/206860533-1c06a2ed-4f60-42b9-95e6-2ad3429a5127.png)

## Now you need a Metamask wallet:

* For this, use a testnet wallet or open a new wallet.
* Click the profile from the top right and click import account
* Enter the key we just got from the PK folder and create the account

![image](https://user-images.githubusercontent.com/101149671/206860604-caebf5ca-f43d-4efd-9ce1-cf6a3e87fab2.png)

## Then we refer to [here](https://itn.qdev.li/)

* Make sure your testnet wallet is correct
* You will get an image like this:
![image](https://user-images.githubusercontent.com/101149671/206860707-60d24966-f27c-4348-90b1-1fd45428df8a.png)


## This is critical and important:
```
CD
cd testnet-public-tools
cd testnet-validator
nano docker-compose.yaml
```

* point to geth's comma, leave a space
Add the * " sign and enter the command with --ethstats in the form
After entering *, add " sign again, add and leave a space
* EXAMPLE: `"geth", "--ethstats=ITN-RuesValidator-9:qstats-testnet@stats.qtestnet.org", ..`
* Exit with CTRL X Y ENTER

![image](https://user-images.githubusercontent.com/101149671/206860778-bd49a825-7c2c-4d68-b5c8-b7a3dd2a2cf4.png)

## We launch:
```
screen -S q
```
```
docker compose up -d
```
```
docker compose logs -f
```

## Let's check from explorer:

* [Explorer](https://stats.qtestnet.org/) is a bit slow and heavy :)
* Color by us:
* It is necessary to wait for half an hour (estimated) to become green
* You become red-yellow-green over time
```
🟢 - You are matched
🟡 - Matching wait a bit
🔴 - Searching for matches
```

-If you have trouble finding your own validator name in Explorer, you can type your own name after ctrl+f and find it. Then, when you hover over the circle next to your own name, which I marked below, and click on the text "click to pin", you will now be able to see your name at the top :)

![kkk](https://user-images.githubusercontent.com/98269269/207414985-60d423e6-facb-4292-be91-999209e9fe29.png)


If you encounter the following error while filling out the form, you need to change the Identify name you use or check your addresses. You can solve this problem by making changes to the characters you use or by checking your validator address.

![dff](https://user-images.githubusercontent.com/98269269/207157285-76e4d6b2-bf65-4155-84b7-59f36fbae211.jpg)


## Diseases are raging, take care of yourself!
