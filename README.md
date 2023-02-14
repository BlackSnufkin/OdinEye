## OdinEye - Discord Cyber Threat Intelligence 
---
![eye_of_Odin](https://user-images.githubusercontent.com/61916899/218772571-1ee47d4c-5a30-4ecc-91b2-463b92e3a9a9.png)
---
### Introduction:

Discord is a platform that can be customized to provide cyber threat intelligence (CTI) professionals with personalized notifications and news updates. This guide will show you how to create a private Discord CTI "Dashboard" using various Discord bots. This server is designed for individual use and is not intended to be made public. It's a simple and effective way to stay informed and up-to-date on the latest developments in Offensive Security World


### Server Setup:

To create your Discord CTI Dashboard, start by setting up a private Discord server. If you're not familiar with how to set up a server, this [guide](https://www.ionos.com/digitalguide/server/know-how/how-to-set-up-a-discord-server/) can walk you through the process.

Once your server is set up, organize it into three main topics: Default Text Channels, Threat Intelligence Channels, and Tool Integration Channels.

The Default Text Channels section should include a few general channels, like a welcome channel, a reminder-bot channel, and an optional chat channel.

The Threat Intelligence Channels section is where you'll create channels for each of the threat intelligence feeds you want to monitor, such as Twitter, Github, YouTube, blogs, and CVE alerts. All alerts from the bots will be sent to these designated channels.

In the Tool Integration Channels section, create channels to receive alerts from various security tools, such as Cobalt Strike.

Here's an example of what your server structure might look like:

-   Default Text Channels
    -   Welcome
    -   Reminder-bot
    -   Chat (optional)
-   Threat Intelligence Channels
    -   Twitter Feed
    -   Github Feed
    -   YouTube Feed
    -   Blogs Feeds
    -   CVE Alerts
-   Tool Integration Channels
    -   Cobalt Strike Alerts

By organizing your server in this way, you can easily access your feeds and alerts, and customize each channel's permissions and roles.

---

### Third-Party Bots 

To furnish these channels with alerts, an array of third-party bots can be leveraged. These bots have been specifically selected for their efficiency, adaptability, and dependability, and can be effortlessly integrated into your Discord server.


|BOT Name|Description|Limitation|
|-----------|------------|----------|
|[TweetShift](https://tweetshift.com/)|Integrates Twitter account to Discord, filtering tweets to certain keywords, and enables tweeting to Twitter within Discord|.Limited to monitoring up to 40 Twitter accounts.|
|[MonitoRSS](https://monitorss.xyz/)| feed monitoring bot for any site that supports RSS we will use it to track Github accounts for specific activities such as repository commits and creations, and can be self-hosted if necessary.|Limited to monitoring up to 5 Github accounts.
|[readybot](https://readybot.io/)|Integrates Discord server with RSS feeds, YouTube, Reddit, and more, and allows filtering of articles to receive.|Limited to monitoring up to 20 websites.
| [YAGPDB](https://yagpdb.xyz/) |multipurpose bot that features fast Reddit and YouTube feeds, self-assignable roles, advanced automoderator, and custom commands.|No major limitations specified.
|[Reminder-Bot](https://reminder-bot.com/dashboard/)|A bot that sends messages at specified times to a designated channel.|No major limitations specified.
|[ProBot](https://probot.io/) |A customizable multipurpose bot that includes welcome images, in-depth logs, social commands, music, moderation, and anti-raid protection.|No major limitations specified.

---

### Self Hosted BOT SetUp:

There are several BOT that can be self-hosted on some VPS or something to get even more alerts and functionality 

#### BOT Name: [ GPT3Discord](https://github.com/Kav-K/GPT3Discord)
- API Nedded:
	-  OpenAI
	- Discord BOT Token
	- DeepL (Optinal)

> A robust, all-in-one GPT3 interface for Discord. Chat just like ChatGPT right inside Discord! Generate beautiful AI art using DALL-E 2! Automatically moderate your server using AI! Upload documents, videos, and files to get AI-assisted insights! A thorough integration with permanent conversation memory, automatic request retry, fault tolerance and reliability for servers of any scale, and much more.

- **Requirements**
	- python3.9 (must be installed recomnded via virtual venv)

- **Installation**
```bash

git clone https://github.com/Kav-K/GPT3Discord.git
cd GPT3Discord/

# Install system packages (python)
sudo apt-get update
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.9
sudo apt install python3.9-distutils

# Install Pip for python3.9
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3.9 get-pip.py

# Install project dependencies
python3.9 -m pip install --ignore-installed PyYAML
python3.9 -m pip install torch==1.9.1+cpu torchvision==0.10.1+cpu -f https://download.pytorch.org/whl/torch_stable.html
python3.9 -m pip install -r requirements.txt
python3.9 -m pip install .
mv sample.env .env

```

##### Create the bot

[https://discordpy.readthedocs.io/en/stable/discord.html](https://discordpy.readthedocs.io/en/stable/discord.html)

-   Create a new Bot on Discord Developer Portal:
    -   Applications -> New Application
-   Generate Token for the app (discord_bot_token)
    -   Select App (Bot) -> Bot -> Reset Token
-   Toogle PRESENCE INTENT:
    -   Select App (Bot) -> Bot -> PRESENCE INTENT, SERVER MEMBERS INTENT, MESSAGES INTENT, (basically turn on all intents)
-   Add Bot the the server.
    -   Select App (Bot) -> OAuth2 -> URL Generator -> Select Scope: Bot, application.commands
    -   Bot Permissions will appear, select the desired permissions
    -   Copy the link generated below and paste it on the browser
    -   On add to server select the desired server to add the bot
-   Make sure you have updated your .env file with valid values for `DEBUG_GUILD`, `DEBUG_CHANNEL` and `ALLOWED_GUILDS`, otherwise the bot will not work. Guild IDs can be found by right clicking a server and clicking `Copy ID`, similarly, channel IDs can be found by right clicking a channel and clicking `Copy ID`.

- Edit the .env file whare all the configuration are stroed and changes them
- Run the bot with `python3.9 gpt3discord.py`
- More Info on [Github Page](https://github.com/Kav-K/GPT3Discord/blob/main/README.md)

---

#### BOT Name: [ MonitoRSS](https://github.com/synzen/MonitoRSS-Clone)

> Repo to deploy the news-delivering bot MonitoRSS (formerly known as Discord.RSS)

- API Nedded:
	- Discord BOT Token
	- Discord Application ID
	- Discord Application Secret

- **Requirements**
	- MongoDB
	- node
	- redis

- **Installation**
```bash

# mongodb install
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

# reddis
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list


sudo apt-get update

sudo apt-get install mongodb-org redis npm

sudo systemctl start mongod.service
sudo systemctl status mongod
sudo systemctl enable mongod

mongosh --eval 'db.runCommand({ connectionStatus: 1 })'

sudo systemctl start redis-server
sudo systemctl status redis-server
sudo systemctl enable redis-server


git clone https://github.com/synzen/MonitoRSS-Clone.git
cd MonitoRSS-Clone 
npm install

```

- **First Run and configuration**
	- Edit the necessary lines in config files 
	- Configs are set in the settings/config.web.json file. If none exist, then you must create one that follows the example at settings/config.web.example.json.
	* Once it all set run with `node bot-web.js`
	- [Documentation](https://docs.monitorss.xyz/)

##### *Config Help

|Config Value|Description|Example|
|------|------------|---------|
|`token`* | Bot token |Generate Token for the app (discord_bot_token) > Select App (Bot) -> Bot -> Reset Token | 
|`redirectURI`* |Domain with `/authorize` appended after it. Make sure you add this exact URL to Redirects for your application at [Discord Developers](https://discordapp.com/developers/applications/), in OAuth2.|in case its run on local Set Both In the config and in the discord developers `http://<YOURE IP>:<PORT>/authorize` **EX.** `http://192.168.1.124:8081/authorize` Select App (Bot) -> OAuth2 and on the main page set the url in the Redirects section|
|`clientID`* | Application ID retrieved from [Discord Developers](https://discordapp.com/developers/applications/). | Select App (Bot) -> OAuth2 then one the main page Copy `CLIENT ID`|
|`clientSecret`* |Application secret retrieved from [Discord Developers](https://discordapp.com/developers/applications/). |Select App (Bot) -> OAuth2 then one the main page Click on `Reset Secret` and copy the output| 


---

#### BOT Name: [BeaconNotifier-Discord](https://github.com/ScriptIdiot/BeaconNotifier-Discord)

> Cobalt strike CNA script to notify you via Discord whenever there is a new beacon.

 - API Nedded:
	 - Discord WebHook
 
 - **Requirements**
	- python3

- **Installation**
	- [Create a Discord Webhook](https://techwiser.com/create-discord-webhook-send-message/)
	- Paste the URL in request.py
	- Edit the path of request.py in notify.cna
	- Edit the message as you want (Optional)
	- Load the cna script via cobaltstrike UI 
	- Wait For inital Connection =)

---

### Resources 

To start receiving alerts with these bots, you can use various news and event feeds as sources. You can find other RSS feeds by searching for the website you're interested in along with "RSS" or "Atom". Alternatively, some websites may have links to their RSS feeds in the footer or elsewhere on the page.

#### Some Feed to start with
 
 - **Blogs-feed**
	- [Infosecurity Magazine](https://www.infosecurity-magazine.com/rss/news/)
	- [BleepingComputer](https://www.bleepingcomputer.com/feed/)
	- [XPNSEC](https://blog.xpnsec.com/rss.xml)
	- [MSRC Blog](https://msrc-blog.microsoft.com/feed/)
	- [SentinelOne](https://www.sentinelone.com/feed/)
	- [Red Canary](https://redcanary.com/feed/)
	- [AT&T Cybersecurity](https://cybersecurity.att.com/site/blog-all-rss)
	- [CISA](https://www.cisa.gov/uscert/ncas/alerts.xml)
	- [NCSC UK](https://www.ncsc.gov.uk/api/1/services/v1/report-rss-feed.xml)
	- [CISecurity](https://www.cisecurity.org/feed/advisories)

- **YouTube-feed**
	- [Computerphile](https://youtube.com/channel/UC9-y-6csu5WGm29I7JiwpnA)
	- [John Hammond](https://youtube.com/channel/UCVeW9qkBjo3zosnqUbG7CFw)
	- [HackerSploit](https://youtube.com/channel/UC0ZTPkdxlAKf-V33tqXwi3Q)
	- [NahamSec](https://youtube.com/channel/UCCZDt7MuC3Hzs6IH4xODLBw)
	- [IppSec](https://youtube.com/channel/UCa6eh7gCkpPo5XXUDfygQQA)

- **Github-Feed**
	- [p0dalirius](https://github.com/p0dalirius.atom)
	- [cube0x0](https://github.com/cube0x0.atom)
	- [CCob](https://github.com/CCob.atom)
	- [rasta-mouse](https://github.com/rasta-mouse.atom)
	- [NUL0x4C](https://github.com/NUL0x4C.atom)

- **Twitter-Feed**
	- [zeropointsecltd](https://twitter.com/zeropointsecltd)
	- [ly4k_](https://twitter.com/ly4k_)
	- [_xpn_](https://twitter.com/_xpn_)
	- [0xBoku](https://twitter.com/0xBoku)
	- [mariuszbit](https://twitter.com/mariuszbit)
	- [mrd0x](https://twitter.com/mrd0x)

- **CVE-Alerts**
- [threatintelctr](https://twitter.com/threatintelctr): In the Tweetshift BOT dashborad add this twitter account and set the channel to `cve-alert`

#### More Resource 
- [awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence#sources)
- [awesome-threat-intel-rss](https://github.com/signalscorps/awesome-threat-intel-rss)
- [ThreatIntelligenceDiscordBot](https://github.com/vxunderground/ThreatIntelligenceDiscordBot)


#### Bonus 	
- [Spyo](https://top.gg/bot/877644741339144244):
	Spyo is a cutting-edge bot designed specifically for professionals in the information technology (IT) sector. With a focus on Cybersecurity, InfoSec, and other tech fields, Spyo offers a range of powerful tools and commands, including OSINT, Cryptography, Forensics, and Recon capabilities. The bot also features CTF hacking challenges that can be played on your server, allowing you to earn certifications for each challenge you complete and join thousands of members on the leaderboard.

- **Telegram Channel Monitoring:**
	Stay up-to-date with the latest news and information from your favorite Telegram channels using RSS feeds generated from public channels. Simply add the channel name to the URL `https://rsshub.app/telegram/channel/<CHANNEL NAME>` to start receiving alerts. For example, to receive updates from the "cveNotify" channel, use the URL `https://rsshub.app/telegram/channel/cveNotify`.


