# how-to-deloy-vue-to-herouku
how-to-deloy-vue-to-herouku
# RUN lines below to deloy a project to heroku app

Make sure you have a little experence person about vue and node js

1. Generate a Vue.js Project
<code>
  npm install --global vue-cli
  vue init webpack <YOUR-PROJECT-NAME-HERE>
  cd <YOUR-PROJECT-NAME-HERE>
  npm install
  npm run dev
 </code>
  
 2. Create Your Heroku App
 <code>heroku create <YOUR-PROJECT-NAME-HERE></code>
  
Lastly, in order to avoid having Heroku install needless development dependencies when deploying later, let’s go ahead and set the NODE_ENV setting to production :
<code>heroku config:set NODE_ENV=production --app <YOUR-PROJECT-NAME-HERE></code>
  
 3. Create a server.js and Build Your Site
 <code>npm install express --save</code>
 
 <code>// server.js
var express = require('express');
var path = require('path');
var serveStatic = require('serve-static');
app = express();
app.use(serveStatic(__dirname + "/dist"));
var port = process.env.PORT || 5000;
app.listen(port);
console.log('server started '+ port);</code>

IMPORTANT: What you probably noticed is that this will serve up a dist directory. 
<code>npm run build</code>

Lastly, we’ll have to edit our start script in package.json to start our node server, as Heroku will automatically look for this script when looking for how to run a node.js app.

<code>
  // package.json
{
  "name": "<YOUR-PROJECT-NAME-HERE>",
  "version": "1.0.0",
  "description": "A Vue.js project",
  "author": "",
  "private": true,
  "scripts": {
    "dev": "node build/dev-server.js",
    "build": "node build/build.js",
    "start": "node server.js",   <--- EDIT THIS LINE HERE 
...
                                      </code>
  4. Git Init and Add Your Heroku Remote Repository
  <code>git init</code>
  
  <code>heroku git:remote --app <YOUR-PROJECT-NAME-HERE></code>
  
  Remove /dist in .gitignore
  <code>
  .DS_Store
node_modules/
dist/  <--- REMOVE THIS LINE
npm-debug.log*
yarn-debug.log*
yarn-error.log*
test/unit/coverage
test/e2e/reports
selenium-debug.log
// Editor directories and files
.idea
*.suo
*.ntvs*
*.njsproj
*.sln
            </code>

Commit to heroku

<code> git add . && git commit -a -m "Adding files." </code>

5. Push Your Code to Deploy!
Now all we need to deploy to Heroku is:

<code>git push heroku master</code>
# See full topic in https://medium.com/netscape/deploying-a-vue-js-2-x-app-to-heroku-in-5-steps-tutorial-a69845ace489
