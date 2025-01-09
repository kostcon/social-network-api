# Social Network API

## Description

This project is a Social Network API built using Node.js, Express.js, MongoDB, and Mongoose. It allows users to create, read, update, and delete data related to users, thoughts, reactions, and friend lists. The API handles large amounts of unstructured data efficiently, making it suitable for social media applications.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [API Routes](#api-routes)
- [Models](#models)
- [Walkthrough Video](#walkthrough-video)
- [License](#license)

## Installation

1. Clone the repository:
    ```bash
    git clone <your-repo-url>
    ```

2. Navigate to the project directory:
    ```bash
    cd social-network-api
    ```

3. Install dependencies:
    ```bash
    npm install
    ```

4. Ensure MongoDB is installed and running on your machine. You can start MongoDB by running:
    ```bash
    mongod
    ```

5. Start the server:
    ```bash
    npm start
    ```
   Alternatively, you can use `nodemon` for development:
   ```bash
   npx nodemon server.js
   ```

## Usage

Use a tool like [Insomnia](https://insomnia.rest/) or [Postman](https://www.postman.com/) to interact with the API. The server runs on `http://localhost:3001` by default.

### Example Endpoints

- GET all users: `GET /api/users`
- GET a single user by ID: `GET /api/users/:id`
- POST a new user: `POST /api/users`
- PUT to update a user by ID: `PUT /api/users/:id`
- DELETE to remove a user by ID: `DELETE /api/users/:id`

## API Routes

### Users

- `GET /api/users`: Retrieve all users.
- `GET /api/users/:id`: Retrieve a single user by ID, including populated thought and friend data.
- `POST /api/users`: Create a new user.
- `PUT /api/users/:id`: Update a user by ID.
- `DELETE /api/users/:id`: Delete a user by ID.
- `POST /api/users/:userId/friends/:friendId`: Add a friend to a user's friend list.
- `DELETE /api/users/:userId/friends/:friendId`: Remove a friend from a user's friend list.

### Thoughts

- `GET /api/thoughts`: Retrieve all thoughts.
- `GET /api/thoughts/:id`: Retrieve a single thought by ID.
- `POST /api/thoughts`: Create a new thought and associate it with a user.
- `PUT /api/thoughts/:id`: Update a thought by ID.
- `DELETE /api/thoughts/:id`: Delete a thought by ID.
- `POST /api/thoughts/:thoughtId/reactions`: Add a reaction to a thought.
- `DELETE /api/thoughts/:thoughtId/reactions/:reactionId`: Remove a reaction by ID.

## Models

### User Model
- `username`: String, unique, required, trimmed.
- `email`: String, required, unique, must match a valid email format.
- `thoughts`: Array of `_id` values referencing the Thought model.
- `friends`: Array of `_id` values referencing the User model.
- Virtual: `friendCount` retrieves the length of the user's friends array.

### Thought Model
- `thoughtText`: String, required, between 1 and 280 characters.
- `createdAt`: Date, default current timestamp, formatted with a getter method.
- `username`: String, required (user who created the thought).
- `reactions`: Array of nested documents created with the `reactionSchema`.
- Virtual: `reactionCount` retrieves the length of the thought's reactions array.

### Reaction Schema (Subdocument)
- `reactionId`: Mongoose's ObjectId, default to a new ObjectId.
- `reactionBody`: String, required, maximum 280 characters.
- `username`: String, required.
- `createdAt`: Date, default current timestamp, formatted with a getter method.

## Walkthrough Video

A walkthrough video demonstrating the functionality of the Social Network API can be found [here](#). The video covers the following:

- Starting the server.
- Demonstrating GET routes for users and thoughts.
- Demonstrating POST, PUT, and DELETE routes for users and thoughts.
- Demonstrating POST and DELETE routes for reactions and friend lists.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

