# [Utopian.io API](https://utopian.io/)
[![GitHub issues](https://img.shields.io/github/issues/utopian-io/api.utopian.io.svg)](https://github.com/utopian-io/api.utopian.io/issues)
[![Contributors](https://img.shields.io/github/contributors/utopian-io/api.utopian.io.svg)](https://github.com/utopian-io/api.utopian.io/graphs/contributors) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/utopian-io/api.utopian.io/pulls) [![GitHub license](https://img.shields.io/github/license/utopian-io/utopian.io.svg)](https://github.com/utopian-io/utopian.io/blob/master/LICENSE)


Node API for Utopian.io.
Utopian wants to reward Open Source contributors for their hard work.

## Installation

1. Fork the repo to your own Github account to allow for submitting pull requests.

2. Make sure you have [NodeJS](https://nodejs.org/), [npm](https://www.npmjs.com/), and [MongoDB](https://www.mongodb.com/) installed. 

3. Download the repo using 
```
git clone git@github.com:[YOUR_GITHUB_NAME]/api.utopian.io.git
``` 
4. Change directory to the project and install dependencies

```
> cd api.utopian.io
> npm install
```

5. Install MongoDB if you do not have it:
- [Mac - MongoDb Install](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)
- [Windows - MongoDB Install](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/)
- [Linux - MongoDB Install](https://docs.mongodb.com/manual/administration/install-on-linux/)

6. Open a new terminal to run your mongoDB server.  This should stop with the message 
`waiting for connections on port 27017` after running the command below
```
> mongod
```

7. Comment the following lines of code in `config/config.js` starting at line 28
```
UTOPIAN_GITHUB_SECRET: Joi.string().required(),
UTOPIAN_GITHUB_CLIENT_ID: Joi.string().required(),
UTOPIAN_GITHUB_REDIRECT_URL: Joi.string().required(),
UTOPIAN_STEEMCONNECT_SECRET: Joi.string().required(),
```
8.  Comment the code in `utopian-bot.js`🤖 below starting at line 19
```
const botAccount = process.env.BOT;
const refreshToken = process.env.REFRESH_TOKEN;
const secret = process.env.CLIENT_SECRET;
const forced = process.env.FORCED === 'true' || false;
```
Paste this below it

```
const botAccount = "utopian-io";
const refreshToken = "";
const secret = "";
const forced = true;
```

9.  You can now run the API server with the command below _(Don't forget to keep your mongoDB instance running)_ This will create your database for you called `utopian-io`
```
> npm run dev-server
```

10. You need to insert a user for yourself in your local mongoDB.  Copy this object and replace capitalized data with your github information:
```
{ 
    "_id" : ObjectId("59f7fd6cdb09066818eb12bc"), 
    "account" : "YOUR_GITHUB_NAME", 
    "github" : {
        "plan" : {
            "private_repos" : NumberInt(0), 
            "collaborators" : NumberInt(0), 
            "space" : NumberInt(976562499), 
            "name" : "free"
        }, 
        "two_factor_authentication" : false, 
        "collaborators" : NumberInt(0), 
        "disk_usage" : NumberInt(2364), 
        "owned_private_repos" : NumberInt(0), 
        "total_private_repos" : NumberInt(0), 
        "private_gists" : NumberInt(0), 
        "updated_at" : "2017-09-28T10:26:29Z", 
        "created_at" : "2015-08-11T09:55:03Z", 
        "following" : NumberInt(0), 
        "followers" : NumberInt(2), 
        "public_gists" : NumberInt(0), 
        "public_repos" : NumberInt(10), 
        "bio" : null, 
        "hireable" : null, 
        "email" : "YOUR_EMAIL", 
        "location" : "YOUR_LOCATION", 
        "blog" : "YOUR_URL", 
        "company" : "YOUR_COMANY", 
        "name" : "YOUR_NAME", 
        "site_admin" : false, 
        "type" : "User", 
        "received_events_url" : "https://api.github.com/users/YOUR_GITHUB_NAME/received_events", 
        "events_url" : "https://api.github.com/users/YOUR_GITHUB_NAME/events%7B/privacy%7D", 
        "repos_url" : "https://api.github.com/users/YOUR_GITHUB_NAME/repos",
"organizations_url" : "https://api.github.com/users/codingdeYOUR_GITHUB_NAMEfined/orgs", 
        "subscriptions_url" : "https://api.github.com/users/YOUR_GITHUB_NAME/subscriptions", 
        "starred_url" : "https://api.github.com/users/YOUR_GITHUB_NAME/starred%7B/owner%7D%7B/repo%7D", 
        "gists_url" : "https://api.github.com/users/YOUR_GITHUB_NAME/gists%7B/gist_id%7D", 
        "following_url" : "https://api.github.com/users/YOUR_GITHUB_NAME/following%7B/other_user%7D", 
        "followers_url" : "https://api.github.com/users/YOUR_GITHUB_NAME/followers", 
        "html_url" : "https://github.com/YOUR_GITHUB_NAME", 
        "url" : "https://api.github.com/users/YOUR_GITHUB_NAME", 
        "gravatar_id" : "", 
        "avatar_url" : "https://avatars1.githubusercontent.com/u/AVATAR_ID?v=4", 
        "id" : NumberInt(13746289), 
        "login" : "YOUR_GITHUB_NAME", 
        "token" : "a3d1046fdfa47f153ed106bacb1cbe548c5c1a16", 
        "account" : "YOUR_GITHUB_NAME"
    }, 
    "createdAt" : ISODate("2017-10-31T04:34:52.639+0000"), 
    "__v" : NumberInt(0)
}
```

Now we can insert this object into the new database that was created by running these commands.  If you have stopped your mongoDB then start it back up so it will serve on port 27017 using 
```
> mongod
```
Switch to another terminal tab and start the mongo shell
```
> mongo
```
Next we need to use the Utopian database
```
> use utopian-io
```
The final step is to insert the object that you created above in the users collection
```
> db.users.insert(
    OBJECT_PASTED_HERE
)
```
11.  Start the API server back up with `npm run dev-server` in the API project director and test that you have github information.


## Tech Stack

- React
- Node.js
- MongoDB


## Contributing
Get in touch on Discord: https://discord.gg/5qMzAJ