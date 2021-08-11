# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```sh
bundle install
rails db:migrate db:seed
rails s
```

Then, in a new terminal, run the frontend:

```sh
npm install --prefix client
npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
  1. Tried submitting form with data
  2. Checked console
    - Saw error message: POST /toys 500 (Internal Server Error)
  3. Checked network tab
    - Saw error message: NameError: uninitialized constant ToysController::Toys
  4. Based on error in network tab, knew there was a typo in the controller
  5. Changed line 10 for the #create method from "toy = Toys.create(toy_params)" to "toy = Toy.create(toy_params)"

- Update the number of likes for a toy

  - How I debugged:
  1. Checked console
    - Saw error message: "Uncaught (in promise) Syntax Error: Unexpected end of JSON input at ToyCard.js:21"
  2. Based on error, knew that controller was not rendering a JSON response for the frontend to use
  3. Added a line to #update method: "render json: toys"

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
  1. Checked console
    - Saw error message: DELETE /toys/2 404 (Not Found)
  2. Checked network tab
    - Saw error message: ActionController::RoutingError: No route matchs [DELETE] \"/toys/2\"
  3. Based on error, knew there was a route missing
  4. Added :destroy as an option to the routes for toys