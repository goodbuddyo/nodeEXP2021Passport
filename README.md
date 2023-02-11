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

// We are using "mongodb": "3.6.6", 




