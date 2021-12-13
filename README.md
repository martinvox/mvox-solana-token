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

Once finished, you'll have to logout and log back in in order to have the PATH variables updated in the shell. Once logged in, you can check your Solana version with:

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



