# Create your own DASH wallet in Ionic 4

- Video to be added

## Introduction - Blockchain, Bitcoin, DASH

Using EC algorithm, a random  private-key, public-key is created. 

Wallet import format(WIF) is created from private-key. WIF is created as it is easy to store/restore.
Refer WIF: https://en.bitcoin.it/wiki/Wallet_import_format

DASH address is created from public-key.
Private-key is used to sign any transactions sent from a address.


While storing a wallet in mobile app, we store WIF. 

Topics needed to continue are 
- DASH address


Example to create random address

https://github.com/dashevo/dashcore-lib/blob/master/docs/examples.md#generate-a-random-address

Functions used to create address
https://github.com/dashevo/dashcore-lib/blob/master/docs/address.md


- DASH wallet

A wallet means just storing a WIF. Then using it any time to get address or private-key from that.

Getting a address from WIF

https://github.com/dashevo/dashcore-lib/blob/master/docs/examples.md#import-an-address-via-wif


Create, Save, Restore Private-key from WIF

https://github.com/dashevo/dashcore-lib/blob/master/docs/examples.md#create-and-save-a-private-key


- DASH WIF

https://github.com/dashevo/dashcore-lib/blob/master/docs/examples.md#create-and-save-a-private-key

## Setup to get DASH javascript library

The DASH javascript library need to be obtained from https://github.com/dashevo/dashcore-lib

You have to create your own browser library. For that do the following

- clone https://github.com/dashevo/dashcore-lib

- npm install (in cloned directory)

- npm run build (in cloned directory)

This will generate files named dashcore-lib.js and dashcore-lib.min.js in the dist/ folder.

Note:- If you try doing "npm install @dashevo/dashcore-lib" and include in mobile app, you may get many missing library errors. So avoid this in this example.



## Setup ionic tabs app

- First time ionic users only
If you are using ionic for first time, refer this link to setup Ionic environment
https://ionicframework.com/docs/installation/cli

Run "npm install -g ionic"

- Create dashwallet tabs app

Run "ionic start dashwallet tabs"



## Refer the template provided

It has 3 tabs,

- Wallet (send and receive)
- Transactions
- Settings (wallet create, set wallet)

## Get some testcoins

Check the balance

## Test by sending/receiving

## Assorted ionic code snippets
- Save wallet WIF
- Read wallet address

## Assorted DASH code snippets

- Create wallet WIF
- Get wallet address from WIF
- Get PrivateKey from WIF
- Do Transaction 


## Understanding DASH libraries 

- Look at the organization 
- See how to access PrivateKey
- See how to access Address
- See how to access Transaction

## REST api to query DASH blockchain

- Example to get balance in DASH address
- Example to get utxo


