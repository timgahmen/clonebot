Clonebot Technical Documentation

◼️ MANDATORY VARIABLES
TG_BOT_TOKEN - Get from @BotFather
APP_ID - Get from my.telegram.org


API_HASH - Get from my.telegram.org


TG_USER_SESSION - Run any userbot session maker


DB_URI = os.environ.get("DATABASE_URL", "")


AUTH_USERS = []


 User string sessions can be generated using any pyrogram V2 compatible session maker, or can be use this repo

◼️ BUTTONS USED IN THIS BOT
    Terminate - To stop the bot from unauthorised usage
    Home - Main menu
    FNAC - File name as caption (This won't work when a custom caption is present)
    CC - Custom caption
    Fr. Id - Clone from message id
    To. Id - Clone to message id
    Source - Source chat (Id, usernames, join links are accepted)
    Target - Target chat (Id, usernames, join links are accepted)
    Delayed - Delay on/off (No delay or 10 Sec delay)
    Caption - Caption on/off (This won't work when a custom caption is present)
    Types - File types to be cloned (Supported- doc, video, audio, photo, voice and text)
    View - To view the current configuration
    Reset - To reset all the things to the bot defaults (All the data will be cleared from the bot)

◼️ TERMS USED IN THIS BOT
    CMID - Current message id
    LMID - Last message id
    FNAC - File name as caption
    CC - Custom caption

◼️ FEATURES
    Configuration using UI
    Anonymous cloning from any chats
    Supports private and public chats
    Bot doesn't need to be a member of chats
    Session user doesn't need to be an admin of the source
    Facility to clone from one to another message ids
    Automatically calculates the last message id of source chat
    Automatically identifies the source and target chat privileges
    Detailed caption facility (Custom, default, file name captions)
    Set custom caption by sending a formatted text to the bot chat
    Delayed - To give a additional layer of protection for your account from getting ban
    Terminate session to protect the unauthorised use of session string
    All types of chat variables are accepted(link, username, Id, Join links)
    Fetch chat id and message id by forwarding a message from a source chat to the bot chat
    Commonly used file types - Doc, Video, Audio, Voice, Photo and Text are supported
    Target chat indexing- To avoid cloning duplicates, bot saves a file with the target conf:
    Duplicate purging - Purging duplicate file while indexing
    Avoiding duplicates - Refer to the above conf: file, bot will avoid cloning of such files
    Reset facility - To delete all the conf: file, can utilise this facility
    Restart facility - Due to some unknown errors, if required, this facility may be beneficial
    Cancel Indexing - If found unwanted, can opt this facility to proceed to clone
    Cancel Clone - To terminate current clone process, this facility may beneficial

◼️ PROCEDURE
    Fork the repository from the main source
    Join the source chat as a user.For public chats, the user doesn't need to be in:Use username instead of id in this case
    Join the target chat as an admin with Posting privileges
    Add source & target chat info to the bot.(If the chat id is not known, Forward any message from any chat to the bot chat.)
    Select the type of files to be cloned
    Add the starting & ending message-ids [Optional]
    Select the other options : [ Optional ]
    Finally, Clone Messages to clone media without forwarding tag
    Finally, Clone Messages to clone media without forwarding tag
    Bot will index the source chat for any duplications. Skip if doesn't required.
    To cancel the process, select 'Cancel' button
    A report text will be generated in the saved messages about the clone process each time
    Speed of Indexing / Clone depends upon the Files age or DC

◼️ DEPLOY

From the last update, clonebot repo needs a database. So, you'll need to have a database installed on your system. I personally use Postgres, so I recommend using it for optimal compatibility.

In the case of Postgres, this is how you would set up a database on a Debian/Ubuntu system. Other distributions may vary.

1. Open terminal as a superuser
sudo su

2. Install PostgreSQL database:
sudo apt-get update && sudo apt-get install postgresq

3. Change to the Postgres user:
sudo su - postgres

4. Create a new database user (change YOUR_USER appropriately):
createuser -P -s -e YOUR_USER_NAME

5. This will be followed by you need to input your password

6. Create a new database table:
createdb -O YOUR_USER YOUR_DB_NAME

7. Create the database with your own values. Change YOUR_USER and YOUR_DB_NAME appropriately.
psql YOUR_DB_NAME -h YOUR_HOST YOUR_USER

This will allow you to connect to your database via your terminal. By default, YOUR_HOST should be localhost:5432

You should now be able to build your database URI. This will be:
sqldbtype://username:pw@hostname:port/db_name

8. An example database URI could be like:
postgresql://johnson:1234@localhost:5432/clonebotdb

9. Create config.py in the main directory. With mandatory variables and database URI. Refer to sample.config or rename it as config.py with your own variables.

Open the main bot directory > right-click > open a terminal here > Or Open a terminal > change to the bot main directory by cd /xxx/xxx

10. Finally, Run the following in the Terminal:
virtualenv -p python3 venv

. ./venv/bin/activate

pip3 install -r requirements.txt

python3 main.py

If everything worked fine, the string session user has a message in this bot 😜


◼️ MANDATORY REQUIREMENT
    String session user must be a member of source chat (Not required for Public chats)
    String session user must be an admin to be the target chat with posting privileges

◼️ UNCERTAINITY

1. Progress Failed to display: When you add a source chat, the bot will automatically find out the last message-id with the supported media types of that chat. In some cases like chats having limitations due to Copywrite infringement or pornography, bot will unable to retrieve the same. So the absence of the last message-id, the bot will fail to calculate the percentage completed and the process history, unless you need to input the same at initial. To avoid the situation, kindly 'VIEW' all fields where okay before beginning the clone.

2. Errors in % or Process bar:

Case-1: This basically occurs when asynchronous message-ids were inserted in starting & ending fields. The bot is calculating the percentage with the value inserted by the user. (Eg: the user inserted an end message id 30 and continued the process. But when in execution, the selected type is ended at message id 28 will cause the percentage to be struck in 90% even when the process has been successfully completed). So, before inserting an end id of a specific type, be sure that the type exists in that id.

Case-2: Bot will automatically set the last message id when a source chat id is added. This will be done according to the presently supported file type defaults in the bot. After you select the file types and go for a clone, the bot will unable to find the last message id depending upon your selection, resulting in errors in percentage. So select filetypes first, then add source. [ Even when in some conditions, the bot will unable to set it right. For a better visual experience, add the last message id manually it doesn't show in VIEW. If you are not selecting any file types, it will be fine at most ]

3.The bot is blocked by the session user: This is a protective mechanism to avoid unauthorised usage of someone's user session string. When a bot like this is deployed somewhere, the session user will send a message in the bot with some text as self. If someone stole a session string and deployed the bot, the session user can find it in this way, and tapping the button 'Terminate' in the bot can terminate the session[Session user only]. After blocking the bot by the session user, will lead to an error message will be printed in the deploy console, every time when tried to deploy with the same bot with the same string. There will be a confirmation for the above command before it takes action. [Heroku will restart the session within 10sec after a session termination, so, the blocking should be done within the time period].

4. Bot not responding: This error basically raised when the files are too older / the DC speed and all. Symptoms are, bot struck in between Indexing / clonning. As the files or dc or the chats configured are not a concern of this bot, there is no other solution for this state. So, it's a humbl request to the users of this bot to restart the bot is an only one solution for the same and please don't raise an issue in the repo or ping with messages in my social media accounts.

To run this bot in a Linux system background refer this documentation.
https://space4renjith.blogspot.com/2024/05/run-your-app-projects-in-system.html

Source: https://space4renjith.blogspot.com/2022/05/clonebot-technical-documentation.html

