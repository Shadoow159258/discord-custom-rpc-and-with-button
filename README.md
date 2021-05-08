# discord-rpc-with-buttons

This guide explains how to make a custom RPC status on Discord!

### Requirements
* You must be logged in to a Discord client in your desktop, so no mobile or web
* You need [Visual Studio Code](https://code.visualstudio.com/) or another code editor
* You need [NodeJS](https://nodejs.org/en/download/) (includes NPM, which is needed as well)

## Step One: Make the application
* Go to the [Developer Portal](https://discord.com/developers/applications) > New Application
* Give it the name you want your RPC status to have
* Under the tab Rich Presence > Art Assets, upload an image (if you want one) and note the name

## Step Two: Creating the project
* Make a new folder and open it in your code editor
* Open a terminal in your project's folder and initialize the project with `npm init -y` (if it gives an error run the interactive setup with `npm init`)
* Install the `discord-rpc` package: `npm install discord-rpc`
* Now, make an `index.js` file and put the following in:
```js
const RPC = require('discord-rpc');
const client = new RPC.Client({
    transport: 'ipc'
});

client.on('ready', () => {
    client.request('SET_ACTIVITY', {
        pid: process.pid,
        activity: {
            details: "Details Here",
            state: "State Here",
            timestamps: {
                start: Date.now()
            },
            assets: {
                large_image: "", // large image key from developer portal > rich presence > art assets
                large_text: "large image text"
            },
            buttons: [
                { label: "Label1", url: "URL1" },
                { label: "Label2", url: "URL2" }
            ]
        }
    });
});

client.login({
    clientId: '', // put the client id from the dev portal here
    clientSecret: '' // put the client secret from the dev portal here
});
```

## Step Three: Running the RPC
* Save all files, then run `node index.js` in the terminal
* It should log that it's ready, and the RPC status should appear on your profile!

Ex : https://cdn.discordapp.com/attachments/829221596102262825/840540209568284712/images_1.jpeg
