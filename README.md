# nodeExp2021Passport


Note: Clone of nodeExp2021Mongo returned no /src/routers folder
If this folder and node_modules are added npm start will work 


------------

Continuation of Pluralsight tutorial 
Building Web Applications with Node.js and Express
by Jonathan Mills

https://app.pluralsight.com/library/courses/nodejs-express-web-applications-building/

How to build from scratch  routing, databases, and third-party APIs in Node.js and Express.

nodeExp2021 is static, without MongoDB


Remember to update package.json
"ejs": "^3.1.8",
 "express": "4.18.2",

cd to directory

	npm install
	npm start
http://localhost:4000/

---------

This part of the project works with
"mongodb": "3.6.6",
and 

mongodb+srv://<username>:<password>@<clustername>...
(find notes for Globomantics)

Remember to update app.js to address deprication warning
app.use(session({ secret: 'globomantics' }));
to
app.use(session({
  secret: 'globomantics',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}))

In local.strategy.js adminRouter.js authRouter.js updated MongoClient params to address warnings
            try {
              client = await MongoClient.connect(url);

            try {
              client = await MongoClient.connect(url, { useUnifiedTopology: true });
---------







