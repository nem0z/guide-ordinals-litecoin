# How to create your first ordinal on Litecoin ?

## Step 1 : Litecoin-core

First step is to install, setup and run litecoin-core.  

You can download litecoin-core from the official web site : https://litecoin.org/fr/  
/!\ Do not select "discard blocks after verification" as you need to store all blocks locally /!\

Syncronize the entier Litecoin blockchain. It will take a few hours, dependings on your network connection and disk speed

If it doesn't create a `litecoin.conf` in the Litecoin folder, create it by yourself or copy the one in the repo

## Step 2 : Install ord-litecoin

Then you need to install `ord-litecoin` from the official repo https://github.com/ynohtna92/ord-litecoin  
It is a fork from the bitcoin `ord` repo modified to works with litecoin

Follow [readme](https://github.com/ynohtna92/ord-litecoin#readme)  
You will need `rustc` (the rust compiler)

You can install with curl :
```bash
    curl --proto '=https' --tlsv1.2 -fsLS https://raw.githubusercontent.com/ynohtna92/ord-litecoin/master install.sh | bash -s
```

or build it by yourself :
```bash
    git clone https://github.com/ynohtna92/ord-litecoin.git
    cd ord
    cargo build --release
```

## Allow and setup RPC connection with litecoin-core

For all the followings steps you will need to run litecoin-core as `ord` works with his RPC api

Configure the `litecoin.conf` file to enable rpc commands and setup credentials :

```
    # server=1 tells Litecoin-QT to accept JSON-RPC commands.
    server=1
    
    # You must set rpcuser and rpcpassword to secure the JSON-RPC api
    rpcuser=<rpc_user>
    rpcpassword=<rpc_password>
```

You will also need to create a `.cookie` at the root of the `Litecoin` folder

```
    <rpc_user:rpc_password>
```

It might be done automaticly when you start litecoin-core  
This file will be used by `ord` to connect to the RPC api  
/!\ It might be delete when you stop litecoin-core /!\

## Create ord wallet

If your Litecoin folder isn't located at the default path, you will need to use the `--litecoin-data-dir` flag to tell `ord` where to find it :

```bash
    ord --litecoin-data-dir ~/Documents/Litecoin
```

Now you can use the `ord` command

Create a wallet :

```bash
    ord wallet create
```

You can see this wallet in litecoin-core, the default name is "ord"  
Don't forget to keep the passphrase in a secure place

Generate a receiving adress : 

```bash
    ord wallet receive
```

Don't forget to send some litecoins to this adress to pay fees, $1 worth of LTC should be enought.

Inscribe a new file as `ordinal` :

```bash
    ord wallet inscribe <path_to_file>
```

It will take a "long" time to index each blocks. It looks like a [PR](https://github.com/ynohtna92/ord-litecoin/pull/1) is open to improve it. Anyway only the first time will take as much time, then you will just need to index new blocks.  

If you have an error about insufifisant transaction fees that doesn't reach to `min relay fees`, you will need to add `--fee-rate 1.1` (or higher).

List all your inscriptions :

```bash
    ord wallet inscriptions
```

## Check tour new ordinal

Current best explorer to see ordinals on litecoin : https://litecoin.earlyordies.com/
https://litecoin.earlyordies.com/inscription/`inscription_id`
