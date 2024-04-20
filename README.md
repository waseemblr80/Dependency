# Dependency
depending
Contribution Requirements
‍
‍You need a computer, ideally Mac or Linux
It is possible on Windows via WSL (which gives you a Linux environment in Windows); instructions for WSL are here: https://learn.microsoft.com/en-us/windows/wsl/install
An old or low-end computer may not be capable of running the ceremony, but we have yet to encounter problems with this so we don’t know the exact specs. You likely need 8 GB of RAM (or more).
A strong internet connection
The most common cause of failures is an inability to upload your contribution to the ceremony before the timeout period expires. Please run the ceremony with a strong internet connection, and in particular one with good upload bandwidth. Using a wired (ethernet) connection rather than a wireless (WiFi) connection is also recommended.
Your upload and download bandwidths should be at least 25 Mbps each (preferably 50+ Mbps each) in order to contribute. There are a number of good speed tests available if you’re unsure (e.g. from Google or Ookla).
Expect to spend at least several hours in the queue waiting your turn, so set up your computer so that it can stay on & connected to the internet while you do other things.
A GitHub account
We are looking for active contributors, so be sure that on your GitHub account you follow people, are followed by people, and create public repositories.
Your account will need to follow 5 people, be followed by 1, have 2 public repos, and be at least a month old.
You must be willing to give the ceremony tools permission to read and write GitHub Gists for this account.
‍

‍

Accessing the Terminal
‍
Contributing to the trusted setup requires access to a terminal window (also called the “command line”) where many commands will be entered. On a mac, you can open the terminal by pressing command-space (aka ⌘+<spacebar>), entering “Terminal” in spotlight search window that opens, and pressing <enter>. (I will assume Linux users have sufficient expertise to adapt these steps for their own particular Linux distro, but if you have any problems please reference the p0tion team’s full documentation or talk to us for help!)

‍

‍

Installing Global Dependencies
‍
Node.js

Download Node.js from https://nodejs.org/en. The “main” LTS version is what we recommend.
Run the installer you just downloaded, and follow the prompts to install.
Node Version Manager (NVM)

Running the CLI app to contribute to the ceremony requires node version 16.20.

We’ll install nvm to change node versions by downloading a shell script using the following command in the terminal:

curl -sL https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh -o install_nvm.sh
This command downloads a file and might look like nothing happened.

Next we’ll install NVM by entering the following command in the terminal:

sh install_nvm.sh
You may need to accept license terms. If it tells you this is required, you will need to run the command it tells you in the terminal; on a mac this will likely be

sudo xcodebuild -license
You will need to follow the prompts, and then repeat the sh install_nvm.sh command again.

If it successfully installs, it will ask you to restart the terminal. If you have any other terminal windows open, first finish your work in them. Now, close the terminal (e.g. with ⌘Q), and re-open it by the same process as before (press ⌘<space>, type “Terminal” into the Spotlight Search bar that this opened, press <enter>).

‍

‍

Contributing to the Ceremony
‍
Step 1 - Create a temporary directory
‍

The first thing to do is to create a temporary directory (folder) to run the ceremony from. I’m going to name it ~/p0tion-tmp in these commands (i.e. a folder named p0tion-tmp in your home directory), but you’re welcome to choose a different name if you prefer.

In the terminal, type

mkdir ~/p0tion-tmp
then hit <enter>. That made your directory, now navigate into it, by typing in the terminal

cd ~/p0tion-tmp
‍

Step 2 - Switch to node v16.20
‍

Before we contribute let’s switch to node v16.20 which the ceremony relies on.

First install the version by entering the following command:

nvm install 16.20
Then use that version by entering:

nvm use 16.20
‍

Step 3 - Install phase2cli
‍

Now you will install the tool that runs the ceremony. Continuing in the terminal, type

npm i @p0tion/phase2cli
‍

Step 4 - Authenticate with GitHub
‍

As described above a GitHub account which meets certain conditions is required to contribute. To authorize your account enter the following command:

npx phase2cli auth
This will copy an authentication code to your clipboard, open your web browser, and take you to a GitHub site asking to give p0tion permission to use the “Gists” feature of your GitHub. Paste the contents of your clipboard into this website and click the button to authorize. GitHub will tell you “Congratulations, you’re all set!” and you can return to the terminal.

‍

Step 5 - Contribute!
‍

You’re ready to contribute to the ceremony. Back in the terminal, enter:

npx phase2cli contribute
You’ll be asked which ceremony to contribute to.

RISC Zero STARK-to_SNARK Prover ceremony should already be highlighted, so press <enter> to select it.

Now, you’ll be asked to choose how to add entropy — this is the secret data for you to destroy and forget (or ideally never know) to secure the ceremony. You can either have it randomly generated or create it manually.

Once you’ve added your entropy, you’ll be placed in the contribution queue. Contributions take a long time, so leave this running in the background or go do something else. (But don’t let your computer go to sleep, a sleeping computer can’t contribute!)

‍

🗣 RETRYING CONTRIBUTIONS

‍If you run into any errors or lose your connection, you can try to restart your contributions by rerunning the npx phase2cli contribute command. Your contribution should continue where it last left off.

‍

Once your contribution is complete, you’ll be invited to share a message on Twitter/X — we encourage you to do so, or on whatever social media platform(s) you prefer! 🎉

‍

Step 6 - Cleanup
‍

After your ceremony contribution completes, it’s probably a good idea to clean up your files and the GitHub authorization. From the terminal, type

npx phase2cli clean
and press <enter>, then type

npx phase2cli logout
and press <enter>, then go to your authorized app list on GitHub and remove the permissions for pse-p0tion-production. You can also delete the ~/p0tion-tmp folder you created if you like.

‍

‍

Common Problems & Troubleshooting
‍
Computer went to sleep: When your turn in the queue comes, your computer needs to be awake and connected to the internet. If you’re going to leave your contribution running and step away from the computer, be sure you don’t have your computer set to automatically sleep
If you disconnect: While in the queue, your spot is saved for you so long as there are still others waiting ahead of you. To re-join, run the npx phase2cli contribute command again and add some new entropy (for security purposes, entropy is not saved between sessions)
Node.js version 16.20: phase2cli is meant to work with node.js version 16.20. This is not the default version on most systems, so you should run nvm use 16.20 before running phase2cli commands. Also, if you restart your terminal you need to run this again.
Running via screen fails: We had a report of tmux succeeding where screen failed. If you’re using screen to make your contribution and hitting mysterious errors, try tmux instead.
Authentication errors: Sometimes phase2cli authentication can get confused, especially if you initially failed the GitHub requirements. To reset authentication, first revoke your p0tion authorization in GitHub, then run phase2cli auth twice (the first run will always fail after revoking), then continue contributing normally.
Cannot rejoin after timeout: If you encounter problems and your contribution window times out, you won’t be able to rejoin the queue immediately. Rejoin again in a few hours (and talk to us if it still doesn’t work).
‍

‍

Speed Run Instructions
‍
The most common cause of failures is insufficient upload bandwidth. Use a system with a good internet connection, and use a wired connection if possible.
Install Node.js and npm if you don’t have them
Run each of the following commands, and follow any prompts they give you (The commands include the example path p0tion-tmp which you may want to adjust)
mkdir p0tion-tmp
cd p0tion-tmp
nvm use 16.20
npm install @p0tion/phase2cli
npx phase2cli auth
# wait two minutes...backend stuff 🤷‍♂️
npx phase2cli contribute
Now let the program run until your contribution is complete!
Once your contribution is complete, you’ll be invited to share a message on Twitter/X — we encourage you to do so, or on whatever social media platform(s) you prefer! 🎉
Use npx phase2cli clean to clean up (and see the cleanup section above for more)
‍

🗣 RETRYING CONTRIBUTIONS

‍If you run into any errors or lose your connection, you can try to restart your contributions by rerunning the npx phase2cli contribute command. Your contribution should continue where it last left off.
