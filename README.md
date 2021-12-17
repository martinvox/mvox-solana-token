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

![image](https://user-images.githubusercontent.com/18686180/146577618-daea2e29-395d-44c9-a1d5-5121c4579f45.png)


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

![image](https://user-images.githubusercontent.com/18686180/146578680-089759ca-3508-4812-b598-fb20bf2c663f.png)

Copy down the Token address, or you can get it later. We just created a token for in the Solana Blockchain, we now need to create an account in order to hold this tokens. To do it, type in the following

* spl-token create-account TOKEN_ADDRESS

![image](https://user-images.githubusercontent.com/18686180/146580379-9d7b0b19-e915-4f1b-969b-1d67a906d096.png)

Now, you got your new account that is holding the token you just created. Next step, we have to fill that account with tokens by minting them. You can make as many tokens you want, or "print" as much as you want. Just type:

* spl-token mint TOKEN_ADDRESS AMOUNT TOKEN_ACCOUNT_ADDRESS

For my case this would be spl-token ApToJQDQ9awk5jaUhJd6ZUQ8f5mbwVtkhmHSoJojkpxc 5000 B9dC4eYzvXurrhAdMXtTiFafC6JUFciysGm9UDNEWrJH

![image](https://user-images.githubusercontent.com/18686180/146580419-bcce212a-2cfc-4b2d-8800-22abb95c1739.png)

If you type:

* spl-tokens account

You should see the token address list and the amount of tokens you actually minted

![image](https://user-images.githubusercontent.com/18686180/146581176-9fca6aa7-a435-4b28-a6f3-ba6564184be1.png)

Lets use and send some tokens to our wallet of preference. To do so:

* spl-token transfer --fund-recipient --allow-unfunded-recipient ApToJQDQ9awk5jaUhJd6ZUQ8f5mbwVtkhmHSoJojkpxc 2000 HcG7HyhJF6oFiBGgAbBRwX8QGnyJc2Schtjtm9a9mYaM

spl-token transfer --fund-recipient --allow-unfunded-recipient ApToJQDQ9awk5jaUhJd6ZUQ8f5mbwVtkhmHSoJojkpxc 2000 HcG7HyhJF6oFiBGgAbBRwX8QGnyJc2Schtjtm9a9mYaM

![image](https://user-images.githubusercontent.com/18686180/146583346-7715390b-ec3b-4eb0-9efc-d5952dee1658.png)


With this, you are transfering tokens from the token account that you created before, to the wallet you just created. Quick note, you will have to put in the parameters --fund-recipient in order for the wallet to receive the tokens and create an account for them, since it will not have one by default. --allow-unfunded-recipient does what it says, allow for this tokens to be sent even if you don't have an account.

If you go to your wallet (I'm using Phantom Wallet) you can see that there is some unknown token. This is the token you just created and sent to your wallet

![image](https://user-images.githubusercontent.com/18686180/146583532-b2b2e9f3-31f8-4e03-bf0b-a47a6bf01c4d.png)

Now that we have our token and token account created, sent some to test, and checked that it is working; it is time to give it a name and assign the correct parameters for it. We can actually see everything on a Solana blockchain explorer like solscan.io or explorer.solana.com

![image](https://user-images.githubusercontent.com/18686180/146584360-c6abcfdb-3618-4b79-9459-d29ef3c658a9.png)

One good practice, after you set up your supply and you have the amount of tokens that you want on circulation, you'll have to run the following command to limit minting:

* spl-token authorize TOKEN_ACCOUNT_ADDRESS mint --disable

![image](https://user-images.githubusercontent.com/18686180/146584917-f7e66ad1-09fd-4d09-8762-2ff111f3835f.png)

And that's it. Time to get rid of the unknown/unrecognized token situation, and we do this by adding it to the Solana Registry. For this, you will need:

* A name
* A symbol
* A logo (try it to be less than 150KB)

First part, is to create a repository in order to upload and store your logo. Go to your main page and click on Create repository or just go to this link https://github.com/new and upload your logo. 

After you are done, you will have to get the raw url from the logo. You can just do it by simply clicking on your uploaded file to see it, and click on download. The copy the link that you will have on the top

![image](https://user-images.githubusercontent.com/18686180/146599541-a1c83af2-7a47-4c78-9ad9-0dc69daccc57.png)

Next step, navigate to the Solana Token list. This is where all the token in the Solana blockhain are listed, and if you want your token to this you will have to do a commit to it. The process is great since it is all automatic.

Go into https://github.com/solana-labs/token-list and fork the repository on the top right.

![image](https://user-images.githubusercontent.com/18686180/146599789-6d181969-2bce-4fbc-8fd7-75ebc47744e6.png)

Once forked, you will have to navigate to the assets folder. Here, each folder represents every token that belong to the Solana Blockchain. In assets, we'll have to create a new folder and name it with our token address. You can do this really easy, by pressing the period Key on your button. This way, Github will load a web version of Visual Studio and it is easier to do this changes.

![image](https://user-images.githubusercontent.com/18686180/146600770-1b8b785c-60c5-4234-901c-4bd773471b7c.png)

After you create the folder that has your token, you will have to upload your logo inside the folder.

![image](https://user-images.githubusercontent.com/18686180/146601179-fc530ef3-39ba-4c9c-b5e1-5f32049f8586.png)

Now, navigate to src/tokens/solana.tokenlist.json. This is the registry of every token that is is in the Solana Blockchain, and where we are going to add our new token. For that, you can copy the syntax of a token that it is already there, and paste it on the bottom of the list.

![image](https://user-images.githubusercontent.com/18686180/146603011-65fe140c-da29-4319-8b94-d269583648e9.png)

I named it Pingüino Anarquista, based on a group of friends that I have. You can name it whatever you want. You will also need to change the address, symbol and logo URL with the raw link, from the logo you uploaded before.

![image](https://user-images.githubusercontent.com/18686180/146603467-09d21e9e-abff-49a8-a0ed-63570e1f7368.png)

Once you are done editing, you will have to commit the changes and check that they were added correctly to your repository.

![image](https://user-images.githubusercontent.com/18686180/146604279-d83950b1-720d-41c6-a869-d08c1c557715.png)

Final steps. Go back to the original Token List repository (https://github.com/solana-labs/token-list) and we will have to merge the changes that we just did to the main repository. Of course, they will have to accept it. If not, you will get a comment saying why. On the top, click on Pull requests:

![image](https://user-images.githubusercontent.com/18686180/146604578-268f42f0-1206-49e5-bd64-f94bff016dbb.png)

Click on new pull request and then on compare across forks

![image](https://user-images.githubusercontent.com/18686180/146604703-fd1dde77-a7f7-4cd9-988b-7a60d42c79a2.png)

![image](https://user-images.githubusercontent.com/18686180/146604749-f42e11bc-6e39-4933-933a-e606c6f62abc.png)









