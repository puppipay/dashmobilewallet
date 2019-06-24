

 npm install @ionic/storage --save

Add storage ans http module
import { IonicStorageModule } from '@ionic/storage';
import { HttpModule } from '@angular/http';

Add import entry
 HttpModule,
 IonicStorageModule.forRoot(),



Copy dashcore-lib.min.js  to  dist/dashcore-lib.min.js

In index.html add
 <script src='dist/dashcore-lib.min.js' type="text/javascript"></script>

Copy puppipay.dash.service.ts

Replace content in tab1.page.html

In tab1.page.ts create logic for send, check balance

# Create your own DASH wallet in Ionic 4

- Video to be added

## Introduction - Blockchain, Bitcoin, DASH
- DASH address
- DASH wallet
- DASH WIF

## Setup to get DASH javascript library

## Setup ionic tabs app

## Take the template provided

It has 3 tabs,

Settings (wallet create, set wallet)

Send/Receive

Transactions

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


