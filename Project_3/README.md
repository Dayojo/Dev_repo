# SIMPLE TO-DO APPLICATION ON MERN WEB STACK

## Step 1
- In order to complete this project, you will need an AWS account and a virtual server with Ubuntu Server OS. When you create your EC2 Instances, you can add Tag "Name" to it with a value that corresponds to a current project you are working on – it will be reflected in the name of the EC2 Instance. Like this:

![0](https://github.com/Dayojo/Dev_repo/assets/123396933/b8c4abd0-49c5-40cc-86cd-1cca550adf63)

## STEP 2 BACKEND CONFIGURATION

`Update ubuntu`

`sudo apt update`

`Upgrade ubuntu`

`sudo apt upgrade`

- Let’s get the location of Node.js software from Ubuntu repositories.

`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

- Install Node.js on the server:

`sudo apt-get install -y nodejs`

- Verify the node installation with the command:

`node -v`

- Verify the node installation with the command:

`npm -v`

![1](https://github.com/Dayojo/Dev_repo/assets/123396933/05f920b6-03ad-46fd-9667-d91a4487f762)

- Create a new directory for your To-Do project:

`mkdir Todo`

- Run the command below to verify that the Todo directory is created with ls command

`ls`

- Now change your current directory to the newly created one:

`cd Todo`

- To initialise your project: 
 
`npm init`

- A new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.

![2](https://github.com/Dayojo/Dev_repo/assets/123396933/17d2fced-782a-45cc-b2a4-53948f2fb24f)

## STEP 3 INSTALL EXPRESSJS

- install it using npm: 

`npm install express`

- Now create a file index.js with the command below:

`touch index.js`

- Run ls to confirm that your index.js file is successfully created:

`ls`

![3](https://github.com/Dayojo/Dev_repo/assets/123396933/2bccfba9-8a91-4719-a2e9-6201cccf86ed)

- Install the dotenv module:

`npm install dotenv`

- Open the index.js file with the command below

`nano index.js`

- Type the code below into it and save. Do not get overwhelmed by the code you see. For now, simply paste the code into the file.

```
const express = require('express');
require('dotenv').config();
 
const app = express();
 
const port = process.env.PORT || 5000;
 
app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});
 
app.use((req, res, next) => {
res.send('Welcome to Express');
});
 
app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```

- Notice that we have specified to use port 5000 in the code. This will be required later when we go on the browser.

- Now it is time to start our server to see if it works. Open the terminal in the same directory as your index.js file and type: node index.js
- If everything goes well, we should see Server running on port 5000 in our terminal.

![4](https://github.com/Dayojo/Dev_repo/assets/123396933/cdde7d60-6117-4ac3-a096-55e7be6a8248)

- Now we need to open this port 5000 in EC2 Security Groups.

![5](https://github.com/Dayojo/Dev_repo/assets/123396933/8728c774-aace-4763-acc9-e8bac50de45f)

![6](https://github.com/Dayojo/Dev_repo/assets/123396933/3a2a17c1-9ace-45a3-a946-301d645caf70)

![7](https://github.com/Dayojo/Dev_repo/assets/123396933/c00db945-d127-49e1-b336-0dfe8f29344b)

![8](https://github.com/Dayojo/Dev_repo/assets/123396933/7c11da84-594b-427c-9776-1201a80357c5)

![9](https://github.com/Dayojo/Dev_repo/assets/123396933/653fcf92-4951-4fd9-b015-d4ffab9f86cd)

![10](https://github.com/Dayojo/Dev_repo/assets/123396933/e2ff820c-223f-406c-9bef-c78dc3bc66fb)

- Now let's open up our browser and try to access our server’s Public IP or Public DNS name followed by port :5000

- Quick reminder how to get your server’s Public IP and public DNS name:

- You can find it in your AWS web console in EC2 details: 

`curl -s http://169.254.169.254/latest/meta-data/public-ipv4`  for Public IP address

`curl -s http://169.254.169.254/latest/meta-data/public-hostname`  for Public DNS name.

`http://<PublicIP-or-PublicDNS>:5000`

![11](https://github.com/Dayojo/Dev_repo/assets/123396933/5689e914-0a68-464e-89cd-8e0cc50d0849)

![12](https://github.com/Dayojo/Dev_repo/assets/123396933/83d3ec45-5395-43ab-b7a5-682834430870)

- There are three actions that our To-Do application needs to be able to do:

  - Create a new task
  - Display list of all tasks
  - Delete a completed task
- Each task will be associated with some particular endpoint and will use different standard HTTP request methods:

  - POST
  - GET
  - DELETE
- For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes mkdir routes

- Change directory to routes folder.

`cd routes`

- Now, create a file api.js with the command below

`touch api.js`

- Open the file with the command below

`nano api.js`

- Copy the code below into the nano editor :

```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```


## STEP 4

- since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model.A schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties.

- To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

    - Change directory back Todo folder with cd .. and install Mongoose `npm install mongoose`
    - Create a new folder models : `mkdir models`
    - Change the directory into the newly created ‘models’ folder with `cd models`
 - All three commands above can be defined in one line to be executed consequently with help of && operator, like this: `mkdir models && cd models && touch todo.js`

paste this in the nano editor todo.js file:

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;

```

- Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model. cd ~
cd to Routes directory, open api.js with: 
`nano api.js`
delete the code inside and paste these code below into it then save and exit:

```

const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');
 
router.get('/todos', (req, res, next) => {
 
//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});
 
router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});
 
router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

```

## STEP 5 MongoDB Database

- To store our data, we require a database. In this case, we will utilize mLab, which offers MongoDB database as a service (DBaaS). To simplify the process, it is recommended to sign up for a free account with shared clusters, which suits our use case perfectly. You can sign up by visiting the provided link. Follow the signup process, and during the procedure, select AWS as the cloud provider and choose a region that is geographically close to your location.

- After signing up, go through the quick guide for getting started. Additionally, we will allow access to the MongoDB database from any location, although it's important to note that this approach is not secure. However, for testing purposes, it serves as an ideal solution.
 
module.exports = router;
