# slack-quizbot

This is a QuizBot to use with [Slack](https://slack.com).

## Installation
```bash
npm install slack-quizbot
```

## Configuration

```javascript
token: "", // Your bot token
admin: [], // List of administrators who can perform special commands. A slack admin is considered as an admin for bot.
autoReconnect: true, // Automatically reconnect after an error response from Slack.
autoMark: true, // Automatically mark each message as read after it is processed.
quizLimit: 25, // Number of questions
quizStartTime: 15, // Time (in seconds) before the first question
quizNextQuestionDelay: 5, // Time (in seconds) before asking the next question
quizBasePoint: 5, // Points earned per question
botCmds: "./src/cmds", // Configuration file (json file) of all commands of the bot. You can change it if necessary.
botMessages: "./src/messages", // File (json file) describing all the boot messages on the channel. You can change it if necessary.
channel: "game", // Channel used for bot
databases: {
    questions: "./data/questions.json", // Path to the database (json file) containing the questions
    scores: "./data/scores.json" // Path to the database (json file) containing scores
}
```

## Usage

```javascript
var Config = {
    token: "xoxb-219955200-k9fdgdfdf565Rt05566f",
    admin: ["U07225LMPB", "U5KJJH0MPL"],
    quizLimit: 45,
    channel: "quizchan",
    databases: {
        questions: "/path/to/questions/questions.json",
        scores: "/path/to/scores/scores.json"
    }
};
var QuizBot = require('slack-quizbot');
var quizbot = new QuizBot(Config);

quizbot.initialize();
```

## Commands

By default the bot will use **src/cmds.json** module to define the commands that can be executed on the channel.
This file may be replaced by your (see [Configuration](#configuration) section) for change the name, description and scope of the command. 
You can also add command aliases such start and begin execute the start function.

### Default commands

* **!enable** : Enable bot
* **!disable** : Disable bot
* **!start** : Start quiz
* **!stop** : Stops current quiz
* **!score** : Displays scores (DM)
* **!myscore** : Displays the user's score (DM)
* **!repeat** : Give current question (DM)
* **!help** : Display help (DM)

### Commands file description :

```javascript
{
    "enable": // command name on the channel
    {
        "desc": "Enable bot", // Command description
        "fn": "enable", // Function to run
        "public": false // Public access or administrator only
    },
    ...
}
```


## Messages

The bot messages are defined in the file **src/messages.json**. This file may be replaced 
with your desired (see [Configuration](#configuration) section).

## Examples

### Questions database

By default the questions database is loaded from the file **data/questions.json** 
whose path is relative to your bot running the file (app.js as in the example). 
An absolute path is recommended.

```json
[
    {"question":"\"Couleur menthe \u00e0 l'eau\" est l'une des chansons de ...","response":"Eddy Mitchell"},
    {"question":"\"Dreaming of me\" est l'un des \"singles\" de quel groupe","response":"Depeche Mode"},
    {"question":"\"Elle & Louis\" est le premier album solo de ....","response":"Louis Bertignac"},
    {"question":"\"La corrida de l'amour\" est le titre japonais d'une c\u00e9l\u00e8bre film, lequel","response":"L'empire de sens"}
]
```

### Scores database

By default the scores database is loaded from the file **data/scores.json** 
whose path is relative to your bot running the file (app.js as in the example). 
An absolute path is recommended.

```json
[
  {"username":"@jean","score":26},
  {"username":"@louis","score":15},
  {"username":"@marie","score":35}
]
```

## Copyright

Copyright &copy; Harouna Madi. MIT License; see LICENSE for further details.