# nodeExp2021Passport


Note: Clone of nodeExp2021Mongo returned no /src/routers folder
If this folder and node_modules are added (npm install) npm start will work 

------------

Continuation of Pluralsight tutorial 
Building Web Applications with Node.js and Express
by Jonathan Mills
nodeExp2021 is static, without MongoDB
nodeExp2021Passport uses "mongodb": "3.6.6",
(see notes for Globomantics) mongodb+srv://<username>:<password>@<clustername>...

  cd to directory
	npm install
	npm start
  http://localhost:4000/

If you address critical and high warnings by updating package.json with:
  "ejs": "^3.1.8",
  "express": "4.18.2",
then res.json(req.user); in authRouter.js will be undefined and login will not work.
---------
we can update: 
app.js to address deprication warning 
// replace // app.use(session({ secret: '******' })); // with

// app.use(session({
//   secret: '******',
//   resave: true,
//   saveUninitialized: true
// }));

// see // https://stackoverflow.com/questions/28839532/node-js-session-error-express-session-deprecated

If no access to mongodb, check if mongodb needs add ip address

In local.strategy.js adminRouter.js authRouter.js updated MongoClient params to address warnings
    try {
      client = await MongoClient.connect(url);

    try {
      client = await MongoClient.connect(url, { useUnifiedTopology: true });

added  autocomplete="username" autocomplete="current-password" to form to address browser warnings
-----------------
Jim Lynch post in PS discussions a year ago:
In Lesson 8: Creating a User: - authRouter.js
If you use MongoDB driver 4.x.x+, be warned collection.insertOne() will no longer return a document, but rather the inserted _id: and acknowledgement. If you want the document, you'll have to .find the document after inserting it:

const results = await db.collection('users').insertOne(user);
debug(results);
const returnedUser = await db.collection('users').findOne({ _id: results.insertedId});
debug(returnedUser);
req.login(returnedUser, () => {
res.redirect('/auth/profile');
});

credit:  https://stackoverflow.com/questions/68555397/return-inserted-document-in-mongodb-node-js

// We are using "mongodb": "3.6.6", although atlas may use 4.x

----------
NOTE!!
/services/speakerService.js references 
        .get('http://localhost:3000/speakers/' + id)
         to call API that references json file.
Would need to update url on prod, and if need pwd, add to gitignore

-----------

app works with original code from lesson, however
11 vulnerabilities (5 moderate, 5 high, 1 critical)
Concerned about undifined error experienced during build that was fixed 
by returning to original package.json

ejs  <3.1.7
Severity: critical
ejs template injection vulnerability - https://github.com/advisories/GHSA-phwq-j96m-2c2q
fix available via `npm audit fix --force`
Install ejs@3.1.8, removed critical issue, app still works

npm install ejs@3.1.8
10 vulnerabilities (5 moderate, 5 high)

for high vulnerabilities, need to upgrade
"express": "4.17.1",
to
"express": "4.18.2",

this may also upgrade "express-session": "1.17.1", which may be a problem
this should also address
"qs": "6.7.0", 
and
 "body-parser": "1.19.0",
 both are in package-lock
body-parser  1.19.0 no longer used in express 4.16+

this install removed high issues, app still works
7 vulnerabilities (5 moderate, 2 high)

upgrade
"nodemon": "2.0.7",
to 
"nodemon": "2.0.20",

this install removed high issues, app still works
1 moderate severity vulnerability











