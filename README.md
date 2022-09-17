# sample_nft_render

Uploading ERC721 on Goerli/Rinkeby Testnet, uploading image and Metadata on IPFS and rendering NFT on Opensea

*** THIS IS A FULL STEP BY STEP TUTORIAL. YOU DO NOT NEED TO CLONE THE REPO ***


Using Truffle, Nodejs, JS, Pinata and Infura.

Note - PLEASE KEEP ALL KEYS PRIVATE AND SAFE!

Installations and Accounts needed:

Node js and VSC installed.

Github login. Link to this repo - 

Metamask setup. Setup rinkeby testnet on metamask and add some test rinkebyEth. 
https://www.alchemy.com/overviews/rinkeby-testnet


Pinata account
https://www.pinata.cloud/

Infura account.
https://infura.io/
 


Steps:

1. Create a folder and open that folder in VSC. 
 
2. Create package.json file by typing in terminal -> npm init -y

3. Install Truffle. In terminal -> npm install truffle.
Run ‘npm audit fix’ to remove vulnerabilities.

4. Run - ‘npx truffle init’

5. In contracts folder, create files ArtCollectible.sol and Migrations.sol. Copy and paste code from Github repo :

6. In migrations folder, create file 1_initial_migrations.js. Copy code from git repo.

7. Install openzeppelin. In terminal -> npm install @openzeppelin/contracts  
(Be careful of typos)
	

8. Create new file in migrations folder 2_deploy_art_collectible.js. Copy code from github.

9. Uploading file to IPFS using pinata. Create account on https://www.pinata.cloud/. 
Click on account symbol on top right and go to API keys and create a key. Copy the key in notes or something. “KEEP IT SAFE AND PRIVATE.”
 
10. Create folder ‘scripts’ in the main directory. Create 3 files ipfsHelper.js, pinFiletoIPFS.js, runScript.js and copy the codes into each of them from the github repo.

11. Create new folder ‘assets’ in the main directory and add the image for your NFT in the folder (in png format).

12. In runScript.js file, change const filepath to ‘../assets/yournftname.png’ where yournftname is the name of the image file in assets.


13. In terminal, run ‘npm i dotenv’ to setup a .env file (which will contain all the keys). Create a file named ‘.env’ in the main directory and copy the code from github.

14. Create a folder in main directory called ‘config’. In there, create a file called ‘dev.json’ and copy the code from github again. 
  Also create an empty folder called ‘data’ in the main directory.

15. Run the following commands in terminal:
Npm install config
Export NODE_ENV=dev

16. In .env file, update PINATA_API_KEY and PINATA_API_SECRET with your own keys from your account. 

17. In terminal, run ‘node scripts/runScript.js’. This will upload image to IPFS and create a file in data folder called ipfsHash.json. It takes about a minute.


18. In data folder, create a new file called metadata.json. Copy the code from github. In image ipfs, replace ”value” in "image": "https://ipfs.io/ipfs/“value” with the value from {"IpfsHash":"value", in ipfsHash.json file in data folder itself. 

19. In runScript.js, comment out the first const filePath with // and remove the second filePath from comments by deleting the // in front of second const.

20. In terminal, run ‘node scripts/runScript.js’. This will upload metadata to IPFS and update the ipfsHash.json in data folder with a second entry. (first entry is image data and second entry is Metadata data on IPFS) It takes about a minute.

21. Login into your infura account and create a new project with network Web3 (for ethereum).
Once setup, under network endpoints and then under Ethereum, click the drop down arrow on mainnet and select rinkeby.
Copy the URL which looks like https://rinkeby.infura.io/v3/……. 
And paste it in the .env file in EthClientURL.

22. Install truffle hdwallet provider by typing in Terminal -> npm i @truffle/hdwallet-provider

23. Now we will be uploading the smart contracts on the testnet. Make sure you have metamask setup, rinkeby testnet added under networks and have some test rinkeby Eth. Link attached on top for this setup.
In metmask, go to account on top right, settings, security and privacy and ask to see the recovery phrase. Copy that phrase and paste in the ‘Mnemonic’ in .env file. (Do not share .env file or keys and phrases with anyone.)

24. Update truffle.config.js by copying code from the same file in github and replacing. 

25. Lets connect to rinkeby network now. In terminal, input command ‘npx truffle develop’ to setup development server and then enter ‘.exit’ to get back to the terminal.

26. Now, lets put the smart contract online. Enter command npx truffle console — network rinkeby’. Note – after npx truffle migrate is - and - twice. After it shows truffle(rinkeby), enter ‘migrate’.

27. After both migrations take place successfully, you’ll see the transactions hashes etc. for each migration. Now after truffle(rinkeby)> enter, ‘const art = await ArtCollectible.deployed()’ which will result in undefined. After this, after truffle(rinkeby)> enter ‘await art.claimItem(‘https://ipfs.io/ipfs/……..’) where ….. Is replaced by IPFS hash of Metadata (second hash in ipfsHash.json file in Data) which looks like QmdrtEjTZCBNxABd3HUXbAh2tmZBWcrnRDsy9YVX7Pgc2T.

28. Congrats, your NFT smart contract has been deployed and your NFT has been transferred to your test wallet. 

29. After truffle(rinkeby)> enter await art.ownerOf(1) and this will result you your metamask wallet address. You’ll also notice that some test Eth have been spent which were used in Migration. 

30. After truffle(rinkeby)>, enter ‘art.address’ which gives the address of the smart contract on chain. Now in the browser enter https://testnets.opensea.io/assets/……./1 where …… is your contract address from art.address command. Here you should see your NFT and info and all the traits along with. 


NOTE FOR FUTURE: I created the same thing using this code but on Goerli testnet as Rinkeby is about to be deprecated (closed) after the merge from first week of October. However, OpenSea testnet is only compatible with the Rinkeby testnet as of now and setup for Goerli should be coming soon.


Feel free to connect or discuss for issues or any help! Thanks
