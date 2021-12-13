# mvox-solana-token

Creating a Solana Token - I have no idea why, I'm just bored. This is based on a few videos and articles I've seen, and wanted to try it myself. 

THIS IS NOT FINANCIAL ADVICE. YOU SHOULD NOT BUY THIS TOKEN BY ANY MEANS. It is just for learning purposes.

NOTE: I'm creating a Token, not a Cryptocurrency. The main difference in these two, is that cryptocurrencies are the native asset of a blockchain like BTC, ETH or SOL whereas tokens are built on an existing blockchain, using smart contracts.

In this case, I'm going to do it in the Solana blockchain since the fees are incredibly low, and the speed of the transaction is almost instant. Solana has a token program written un Rust, that will allow you to create your own token really easily. 

What are we going to need ?

* Linux, Windows or a Mac
* Basic knowledge of cli
* Know your way around GitHub
* Some SOL. You can buy this through an exchange.


For the Linux Machine, I'm going to use WSL in Windows 11. To install it, just run wsl --install on Powershell with administrator rights. For more info, check: https://docs.microsoft.com/en-us/windows/wsl/install


Another good option is the free ARM Ubuntu based VM on Oracle Cloud. Why Oracle Cloud ? It is free and runs super smooth. You can set up your account in the following link: https://www.oracle.com/cloud/

Once you set up your VM with Ubuntu (I used WSL), login via SSH or your preferred way.

![image](https://user-images.githubusercontent.com/18686180/145824668-2f4eee32-9503-4e36-8462-68a84ab16717.png)

Once connected, the first thing to do is Install the <a href="https://docs.solana.com/cli/install-solana-cli-tools">Solana CLI Tools</a>. Copy and paste the following:

sh -c "$(curl -sSfL https://release.solana.com/v1.9.0/install)"

You can replace v1.9.0 with the release tag you want, or use one of the three symbolic channel names: stable, beta or edge.

![image](https://user-images.githubusercontent.com/18686180/145827554-f29efe2b-938b-4151-b527-6e010d759729.png)

Once finished, you'll have to logout and log back in, in order to have the PATH variables updated in the shell. Once logged in, you can check your Solana version with:

solana --version

![image](https://user-images.githubusercontent.com/18686180/145827928-7eb0ba91-88b6-4094-a9dd-cbd71ed84257.png)

Next step, is to create our cryptocurrency wallet that will have some Solana, in order to make some transactions. 

Remember, you will only need around 5 bucks no more than that. It is good to clarify, that if you purchase SOL in an exchange, lets select Coinbase, it will requiere a minimum of 0.005 SOL in order for the withdrawal to happen. This is around 15/20 USD.

To create a new wallet, just run the following command:

solana-keygen new

![image](https://user-images.githubusercontent.com/18686180/145828770-c57fb67a-0f7f-4adb-afd4-71c58cac7829.png)

We just created a Solana wallet, with one command. You will see that your keypair was saved in a json file, that is were your private key is. Below, you will have your public key. That's the wallet address where you want people to send you some Solana, and where we are going to send some in a few moments.

One of the most important thinks is the seed phrase that you want to write down in a piece of paper and save it. I can't stress this enough, it is not recommended to save it anywhere else than in a physicall way. If you store it in the Cloud, and someone gets access to your machine you will risk yourself to loose all the tokens you have in that wallet. In case something happens to the computer/VM where you are working right now, you'll be able to recover this wallet with this seed phrase.

You can check it out on the <a href="https://explorer.solana.com/address/B88mrEVoLW9z5ZJsteF6VfKczL6genDi47AoeE3NYz2b">Solana Blockchain Explorer</a>, if you search for my wallet address B88mrEVoLW9z5ZJsteF6VfKczL6genDi47AoeE3NYz2b, you'll se that it has some SOL.

![image](https://user-images.githubusercontent.com/18686180/145830100-efc33a97-d851-4c33-b64a-fe647cd1a620.png)

We will need some more stuff installed on the VM right now. First, do a sudo apt update to update the repos.

After that we'll install Rust, the language that Solana uses in order to create and deploy tokens. To install it, copy and paste this command:

curl https://sh.rustup.rs -sSf | sh

We'll continue with the default installation since that is more than necessary.

![image](https://user-images.githubusercontent.com/18686180/145863325-40bdfe99-7d9b-43b3-85d7-0b99504a2422.png)

It will take a bit of time to get it done, but once finished you should see something similar to this:

![image](https://user-images.githubusercontent.com/18686180/145863386-59e21aa2-4a5f-4744-8bc5-2943962225bb.png)

Log out, and log back in to update the variables. Sane as last time.

We need to install a few other prerequirements:
* libudev-dev contains the files needed for developing applications that use libudev. 
* libssl-dev is part of the OpenSSL project's implementation of the SSL and TLS cryptographic protocols for secure communication over the Internet. It contains development libraries, header files, and manpages for libssl and libcrypto. 

You can install both with:
* sudo apt install libudev-dev
* sudo apt install libssl-dev pkg-config

Last but not least you need build-essential (this was already preinstalled on WSL)

* sudo apt install build-essential -y

![image](https://user-images.githubusercontent.com/18686180/145864486-5212fa50-395e-4fab-98a0-69321e8e5bf1.png)

Next step, <a href="https://spl.solana.com/token">install Solana's token program</a>. This is a CLI tool that will allows us to install a token in the Solana blockchain. To install it, run the following command with cargo (this is from Rust.)

* cargo install spl-token-cli

Once finished, you should see something like this

![image](https://user-images.githubusercontent.com/18686180/145865720-0745f02f-f94b-4964-8364-f2019a61d8ef.png)

Now, it is time to purchase some Solana and send it to your wallet that we created before. Mine is B88mrEVoLW9z5ZJsteF6VfKczL6genDi47AoeE3NYz2b. You can buy it from Binance, Coinbase and other several exchanges. Once you sent some Solana to that wallet, we can proceed to the fun part.

Time to create the token. Good thing about Solana, is that everything is "pre-built" and with everything that we installed so far, you should be able to create your token with a simple command:

* spl-token create-token
