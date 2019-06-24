# Create your own DASH wallet in Ionic 4


## Video 

[![Working of DASH wallet](https://img.youtube.com/vi/Wj8mJYc0Nlc/0.jpg)](https://www.youtube.com/watch?v=Wj8mJYc0Nlc "Working of DASH wallet")


## Source of the DASH wallet 

 https://github.com/puppipay/workingdashwallet/


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

-- https://github.com/dashevo/dashcore-lib/blob/master/docs/examples.md#generate-a-random-address

Functions used to create address

-- https://github.com/dashevo/dashcore-lib/blob/master/docs/address.md


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

Run command

npm install -g ionic

- Create dashwallet tabs app

Run "ionic start dashwallet tabs"

 npm install @ionic/storage --save

- Add storage and http module to ionic application

import { IonicStorageModule } from '@ionic/storage';
import { HttpModule } from '@angular/http';

- Add import entry for ionic application

 HttpModule,
 IonicStorageModule.forRoot(),


- Copy dashcore library to appropriate place

Copy dashcore-lib.min.js  to  dist/dashcore-lib.min.js

In index.html add

 <script src='dist/dashcore-lib.min.js' type="text/javascript"></script>





## Refer the template provided

It has 3 tabs,

- Wallet (send and receive)
- Transactions (see sent transaction)
- Settings (wallet create, set wallet)

## Get some DASH testcoins

``` bash
It can be loaded from one of the link below


http://test.faucet.masternode.io/
http://faucet.test.dash.crowdnode.io/

```

## Verifying DASH testnet address has balance 

``` bash
In below link replace the address with your DASH testnet address

https://testnet-insight.dashevo.org/insight-api/addr/92wN1HFM2qmarbxwN25EeeTC4iiF1dZzcx


```

## Test by sending/receiving

- See the video of sending DASH.

- For receiving DASH into your wallet, provide the "wallet-address" to the other sending application.

## Assorted ionic code snippets

- WIF to address

``` bash
wiftoaddress() {

  this.walletaddress = dashcore.PrivateKey.fromWIF(this.walletwif ).toAddress(dashcore.Networks.testnet).toString();

}

```

- Save wallet WIF

``` bash
savewif() {

   this.wiftoaddress() ;
   this.storage.set('walletwif', this.walletwif);

}

```

- Load wallet WIF

``` bash
loadwalletwif() {
     this.storage.get('walletwif').then(data=> {
        if(data) {
      this.walletwif = data;
      this.wiftoaddress() ;
      this.gettestnetbalance() ;
        }
     });
}


```


## Assorted DASH code snippets used

- Create wallet WIF

``` bash
 var privateKey = new dashcore.PrivateKey();
  this.walletwif = privateKey.toWIF();

```

- Get wallet address from WIF

``` bash
  this.walletaddress = dashcore.PrivateKey.fromWIF(this.walletwif ).toAddress(dashcore.Networks.testnet).toString();

```
- Get PrivateKey from WIF

``` bash
 privatekey =  dashcore.PrivateKey.fromWIF(this.walletwif );

```

- Perform DASH Transaction 

``` bash
  var tx = new dashcore.Transaction()
      .from(utxo)
      .to([{address: toaddress, satoshis: toamount}])
      .fee(fees)
      .change(changeaddress)
      .sign(privatekey);


```

## Understanding DASH libraries 

- Look at the organization of DASH library

-- https://github.com/dashevo/dashcore-lib/blob/master/index.js

- See how to access PrivateKey

Observe Privatekey library is exported as below

``` bash
bitcore.PrivateKey = require('./lib/privatekey');
```

So when PrivateKey functionality has to be accessed, it is done as below

``` bash
dashcore.PrivateKey.fromWIF(...)
```

- See how to access Transaction

Observe Transaction library is exported as below

``` bash
bitcore.Transaction = require('./lib/transaction');

```
Similarly Transaction is accessed as

``` bash

var tx = new dashcore.Transaction()...

```


## REST api to query DASH blockchain

- Example to get balance in DASH address

Refer: source provided https://github.com/puppipay/workingdashwallet/blob/master/src/app/providers/puppipay.dash.service.ts

``` bash
getBalance(address: string, network: string): any {

     var url ;

     if(network == 'testnet') {
        url = 'https://testnet-insight.dashevo.org/insight-api/addr/';
     }
     else {
        url = 'https://insight.dashevo.org/insight-api/addr/';
     }

     return new Promise((resolve, reject) => {


     this.http.get(url+address).subscribe(res => {
                let data = res.json();
                resolve(data);
        }, (err) => {
          reject(err);
        });
    });


  }


```

- Example to get utxo

Refer: source provided https://github.com/puppipay/workingdashwallet/blob/master/src/app/providers/puppipay.dash.service.ts

``` bash
  getUtxo(address: string, network: string): any {

     var url ;

     if(network == 'testnet') {
        url = 'https://testnet-insight.dashevo.org/insight-api/addr/';
     }
     else {
        url = 'https://insight.dashevo.org/insight-api/addr/';
     }

     return new Promise((resolve, reject) => {


     this.http.get(url+address+"/utxo").subscribe(res => {
                let data = res.json();
                resolve(data);
        }, (err) => {
          reject(err);
        });
    });


  }


```


- Example to build transaction

Refer: source provided https://github.com/puppipay/workingdashwallet/blob/master/src/app/providers/puppipay.dash.service.ts

``` bash
 createtransaction(utxo, privatekey,changeaddress, toaddress, toamount,fees) {

  var tx = new dashcore.Transaction()
      .from(utxo)
      .to([{address: toaddress, satoshis: toamount}])
      .fee(fees)
      .change(changeaddress)
      .sign(privatekey);

  var txobject = tx.toBuffer();

   return txobject;
 }


```
