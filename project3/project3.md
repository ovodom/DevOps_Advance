# PROJECT 3

# ELITE CORPORATION API

## PREFACE: 

This project is about creating a lightweight task management API that can run in a Docker container without requiring a database. 
REQUIRMENTS (EMPLOYEES TO):

1.	 Add new task
2.	View all task
3.	Update task status 
4.	Delete tasks

## SETTING UP PROJECT

1.	Create an EC2 instance and SSH into its terminal.



![img](img/img1.png)



![img](img/img2.png)



![img](img/img3.png)




2.	Sudo apt update to update packages on Debian based (ubuntu) system and 
3.	Run the following command to create elite-task-api and change directory to elite-task-api

```
   mkdir elite-task-api
   cd elite-task-api
```



![img](img/img4.png)




4.	To initialize Node.js project: 
a.	Install npm sudo apt install npm



![img](img/img5.png)




b.	Run command npm ```init –y``` to create package.json



![img](img/img6.png)




c.	Run command ```npm install express``` to install necessary dependencies for express



![img](img/img7.png)




![img](img/img8.png)




5.	Run command ```vi app.js``` to create app.js file and paste the configuration

```
// app.js

const express = require('express');
const app = express();
app.use(express.json()); // This is to parse JSON bodies

let tasks = [
  { id: 1, title: "Fix server issue", status: "Pending" },
  { id: 2, title: "Deploy new feature", status: "Completed" }
];

// POST /tasks - Add a new task
app.post('/tasks', (req, res) => {
  const { title } = req.body;
  const id = tasks.length + 1; // Generate new ID
  const newTask = { id, title, status: "Pending" };
  tasks.push(newTask);
  res.status(201).json(newTask);
});

// GET /tasks - Get all tasks
app.get('/tasks', (req, res) => {
  res.json(tasks);
});

// PUT /tasks/:id - Update a task
app.put('/tasks/:id', (req, res) => {
  const { id } = req.params;
  const { title, status } = req.body;
  const task = tasks.find(t => t.id === parseInt(id));

  if (!task) return res.status(404).send('Task not found');
  
  task.title = title || task.title;
  task.status = status || task.status;
  
  res.json(task);
});

// DELETE /tasks/:id - Delete a task
app.delete('/tasks/:id', (req, res) => {
  const { id } = req.params;
  const taskIndex = tasks.findIndex(t => t.id === parseInt(id));

  if (taskIndex === -1) return res.status(404).send('Task not found');

  tasks.splice(taskIndex, 1);
  res.status(204).send();
});

// Set up the server
const port = 3000;
app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});

```




![img](img/img9.png)




![img](img/img10.png)




•  POST /tasks: Adds a new task. You send the task title in the request body.
•  GET /tasks: Returns all the tasks.
•  PUT /tasks/:id: Updates a task by its ID. You send the new title or status.
•  DELETE /tasks/:id: Deletes a task by its ID.

6.	Let us Dockerize the application by creating a Dockerfile with the command ``` vi Dockerfile``` and paste the following:

```
# Use official Node.js 18 Alpine image
FROM node:18-alpine

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application files
COPY . .

# Expose port 3000 to the outside world
EXPOSE 3000

# Command to run the app
CMD ["node", "app.js"]

```




![img](img/img11.png)




![img](img/img12.png)





 This Dockerfile is telling Docker how to build the image:

•	It starts from the node:18-alpine base image.

•	Copies the package.json and package-lock.json files into the container.

•	Installs the dependencies (npm install).

•	Copies the rest of the application files.

•	Exposes port 3000 so that the API can be accessed from outside the container.

•	Finally, it starts the app by running node app.js.


7.	Create a .dockerignore file to make sure you don't copy unnecessary files into the Docker image (like node_modules):

a.	Paste this on the file 

```
node_modules 
npm-debug.log
```




![img](img/img13.png)





8.	Install docker ```sudo apt install docker.io``` and build docker image using the following command
```docker build -t elite-task-api``` .



![img](img/img14.png)



![img](img/img15.png)




![img](img/img19.png)





This will read your Dockerfile and create an image named elite-task-api.

** NOTE: If permission to proceed is denied use the following commands to change the user (grant access) ```sudo usermod -aG docker $USER``` and ```newgrp docker``` to keep system running.   




![img](img/img16.png)




![img](img/img17.png)





9.	After building the image, run container with this command, ```docker run -p 3000:3000 elite-task-api```




![img](img/img20.png)




![img](img/img21.png)




This command tells Docker to run the elite-task-api image and map the container's port 3000 to your local machine's port 3000.


10.	Edit inbound rule of EC2 instance. Do a drop down and add  

•  Type: Custom TCP Rule

•  Port Range: 3000

•  Source: Anywhere (or specify a range) and save the changes made.
 



![img](img/img22.png)






11.	Test Elite Corporation API on postman : Test the POST /tasks Endpoint (Add a new Task):

a.	•  Open Postman and create a new request by     clicking on the New button and selecting Request.

b.	•  Set the HTTP method to POST.

c.	•  In the URL field, enter your EC2 instance’s public IP with port 3000, like this:
http://<EC2_PUBLIC_IP>:3000/tasks

d.	Go to the body, enter a JSON object representing the task you want to add, like this:

```
{
  "title": "Prepare quarterly report"
}

```


e.	Click send. Expected result: a response with the task data you just added, including the generated id, like this:
                              
```

                              {
  "id": 3,
  "title": "Prepare quarterly report",
  "status": "Pending"
}

```



![img](img/img23.png)





12.	Test the GET /tasks Endpoint (Get All Tasks)
a.	Create a new request in Postman, set the method to GET, and enter the following URL:
http://<EC2_PUBLIC_IP>:3000/tasks

b.	Click send.
Expected Result: You should receive a response with an array of all tasks, like this:

```
[
  {
    "id": 1,
    "title": "Fix server issue",
    "status": "Pending"
  },
  {
    "id": 2,
    "title": "Deploy new feature",
    "status": "Completed"
  },
  {
    "id": 3,
    "title": "Prepare quarterly report",
    "status": "Pending"
  }
]

```



![img](img/img24.png)





13.	Test the PUT /tasks/:id Endpoint (Update a Task):

Create a new request in Postman, set the method to PUT, and enter the URL with the specific task ID you want to update. For example, to update the task with ID 1:
http://<EC2_PUBLIC_IP>:3000/tasks/1

•  Go to the Body tab, select raw, and set the data type to JSON.

•  Enter the new data you want to update. For example, to change the status of the task to "Completed":


```
{
  "status": "Completed"
}
```


•	Click Send.
Expected Result: You should receive a response with the updated task data, like this:



```
{
  "id": 1,
  "title": "Fix server issue",
  "status": "Completed"
}
```





![img](img/img25.png)






14.	Test the DELETE /tasks/:id Endpoint (Delete a Task):

Create a new request in Postman, set the method to DELETE, and enter the URL with the task ID you want to delete. For example, to delete the task with ID 3:
http://<EC2_PUBLIC_IP>:3000/tasks/3

•	Click Send.
Expected Result: You should receive a 204 No Content status with no response body, indicating the task has been successfully deleted.





![img](img/img26.png)