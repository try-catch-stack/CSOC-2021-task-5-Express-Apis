# Todo App API - CSoC Dev Task 5

## Introduction

Welcome to the Week 5 of CSOC Dev. In this assignment, you will be working on the Express Framework. You will be implementing the same API server which we created for you in the Task 1. Also, you will be adding some additional functionality to the API.


### Setting up the project

- Fork and clone this repo.
- Go the project folder in terminal and run `yarn` to install all dependencies.
- Run `yarn connectDB`to connect to the DB.
- Start the development server using `yarn dev`.
- Server should automatically reload and reflect your changes upon saving, if that doesn't happen quit the server using `ctrl+c` and restart development server.
- Install postman/insomnia for processing the requests.

### Working
The API which we had created for Task 1 is deployed at https://todo-app-csoc.herokuapp.com/.

You'll have to complete two subtasks:

- **Complete all the basic endpoints (API Description is included below)**:

  Auth - Login, Register, Get Profile and Todo - Get Detail, Get List, Create, Edit and Delete.You will also have to add the middleware function for authorization. In this subtask, only the creator of the Todo will have the access to View, Edit or Delete the Todo. 

- **Implement collaborator feature**:

  In this subtask, you will have to implement a feature where the creator of a todo can add or remove the collaborators to a todo. Specifically, for every todo, the owner can add one or more collaborator to a todo and can remove one or more collaborators from a todo. So, every todo will have a set of collaborators (may be empty too). The collaborator of a todo will have the access to Edit or Delete the todo, but he won't be able to add or delete the collaborators to the todo. Only the creator of the todo will have the permission to add or remove collaborators.
  
  For this subtask, you may need to fiddle around with the models, create some views and serializers and make the necessary endpoints. We suggest you to create the two endpoints `/todo/:id/add-collaborators/` and `/todo/:id/remove-collaborators/` for adding and removing collaborators, respectively. Also, you will need to modify the GET Todo endpoint to display all the Todo - the one which the user has created, and the one for which the user is collaborating. Make sure to distinguish between the two of them, and we leave your imagination on how to do this.
  
Make sure to do proper validation of the requests, and grant proper permissions to a user.

## Tasks
- ### Complete all the basic endpoints (100 points)
- ### Collaborator feature (100 points)

## Deadline
You'll have a week to complete this task. Hence, the deadline of this task is 15th May, 2020.

## Submission
* Follow the instructions to setup and run this project.
* Complete the task by making the required changes in the files.
* When done, commit your work locally and push it to your origin (forked repository).
* Make a pull request to our repository, stating the tasks which you have completed.
* Let us review your pull request.

## API Description (Only for Subtask 1)

### Auth System
For this API, you will have to use Token-based Authorization. We have already created a model named **Token**  required to create token for a user, for your reference. All the requests made to the API (except the Login and Register endpoints) shall need an  *Authorization header*  with a valid token and the prefix  *Token*. Make sure to add proper permissions in the views to implement this.

For authorization, a `createToken()` has been created in the `controllers/user.js`. Generally we use jwt for authentication but here we have created a model for the same.

In order to obtain a valid token it's necessary to send a request  `POST /auth/login/`  with  **username**  and  **password**. To register a new user it's necessary to make a request  `POST /auth/register/`  with name, email, username and password.

### End Points

**Auth**

-   `POST /auth/login/` 

	Takes the username and password as input, validates them and returns the **Token**, if the credentials are valid.  
  
	Request Body (Sample):
	```
	{
	  "username": "string",
	  "password": "string"
	}
	```
	Response Body (Sample):
	```
	{
	  "token":  "string"
	}
	```
	Response Code: `200`
	
-   `POST /auth/register/`

	Register a user in Django by taking the name, email, username and password as input.
  
	Request Body (Sample):
	```
	{
	  "name": "string",
	  "email": "user@example.com",
	  "username": "string",
	  "password": "string"
	}
	```
	Response Body (Sample):
	```
	{
	  "token":  "string"
	}
	```
	Response Code: `200`
	
-   `POST /auth/profile/`

	Retrieve the id, name, email and username of the logged in user. Requires token in the Authorization header.
  
	Response Body (Sample):
	```
	{
	  "id":  1,
	  "name":  "string",
	  "email":  "user@example.com",
	  "username":  "string"
	}
	```
	Response Code: `200`


**Todo**

-   `GET /todo/`

	Get all the Todos of the logged in user. Requires token in the Authorization header.
  
	Response Body (Sample):
	```
	[
	  {
	    "id":  1,
	    "title":  "string"
	  },
	  {
	    "id":  2,
	    "title":  "string"
	  }
	]
	```
	Response Code: `200`

-   `POST /todo/create/` **(The Response Body of this endpoint is different from what we have created for Task 1)**

	Create a Todo entry for the logged in user. Requires token in the Authorization header.
  
	Request Body (Sample):
	```
	{
	  "title": "string"
	}
	```
	Response Body (Sample):
	```
	{
	  "id":  1,
	  "title":  "string"
	}
	```
	Response Code: `200`

-   `GET /todo/:id/`

	Get the Todo of the logged in user with given id. Requires token in the Authorization header.
  
	Response Body (Sample):
	```
	{
	  "id":  1,
	  "title":  "string"
	}
	```
	Response Code: `200`

-   `PUT /todo/:id/`

	Change the title of the Todo with given id, and get the new title as response. Requires token in the Authorization header.
  
	Request Body (Sample):
	```
	{
	  "title": "string"
	}
	```
	Response Body (Sample):
	```
	{
	  "id":  1,
	  "title":  "string"
	}
	```

-   `PATCH /todo/:id/`

	Change the title of the Todo with given id, and get the new title as response. Requires token in the Authorization header.
  
	Request Body (Sample):
	```
	{
	  "title": "string"
	}
	```
	Response Body (Sample):
	```
	{
	  "id":  1,
	  "title":  "string"
	}
	```

-   `DELETE /todo/:id/`

	Delete the Todo with given id. Requires token in the Authorization header.
  
	Response Code: `204`

### Testing the API

The API can be tested by running the NodeJS server locally, going to the following url: [http://127.0.0.1:8000/](http://127.0.0.1:8000/), clicking the "Try it out" button after selecting the endpoint and finally executing it along with the Response Body (if required).

For testing the endpoints which require **Token** in the Authorization header, you can click on the "Authorize" button, write the Authorization token as  `Token <token>` (which you have obtained from the `auth/login/` endpoint) and finally click on "Authorize". Thereafter, all the requests made to any endpoint will have the Token in the Authorization Header.
