# User Story

## As an Avid Reader
I want to search for new books to read so that I can keep a list of books to purchase.

## Acceptance Criteria
**Given** a book search engine

1. **When** I load the search engine
   - **Then** I am presented with a menu with the options Search for Books and Login/Signup, an input field to search for books, and a submit button

2. **When** I click on the Search for Books menu option
   - **Then** I am presented with an input field to search for books and a submit button

3. **When** I am not logged in and enter a search term in the input field and click the submit button
   - **Then** I am presented with several search results, each featuring a book’s title, author, description, image, and a link to that book on the Google Books site

4. **When** I click on the Login/Signup menu option
   - **Then** a modal appears on the screen with a toggle between the option to log in or sign up

5. **When** the toggle is set to Signup
   - **Then** I am presented with three inputs for a username, an email address, and a password, and a signup button

6. **When** the toggle is set to Login
   - **Then** I am presented with two inputs for an email address and a password and a login button

7. **When** I enter a valid email address and create a password and click on the signup button
   - **Then** my user account is created, and I am logged in to the site

8. **When** I enter my account’s email address and password and click on the login button
   - **Then** the modal closes, and I am logged in to the site

9. **When** I am logged in to the site
   - **Then** the menu options change to Search for Books, an option to see my saved books, and Logout

10. **When** I am logged in and enter a search term in the input field and click the submit button
    - **Then** I am presented with several search results, each featuring a book’s title, author, description, image, and a link to that book on the Google Books site, and a button to save a book to my account

11. **When** I click on the Save button on a book
    - **Then** that book’s information is saved to my account

12. **When** I click on the option to see my saved books
    - **Then** I am presented with all of the books I have saved to my account, each featuring the book’s title, author, description, image, and a link to that book on the Google Books site, and a button to remove a book from my account

13. **When** I click on the Remove button on a book
    - **Then** that book is deleted from my saved books list

14. **When** I click on the Logout button
    - **Then** I am logged out of the site and presented with a menu with the options Search for Books and Login/Signup, an input field to search for books, and a submit button

## Mock-Up
Let's start by revisiting the web application's appearance and functionality.

As you can see in the following animation, a user can type a search term (in this case, "star wars") in a search box and the results appear:
![Alt text](image.png)

Animation shows "star wars" typed into a search box and books about Star Wars appearing as results.

The user can save books by clicking "Save This Book!" under each search result, as shown in the following animation:
![Alt text](image-1.png)

Animation shows user clicking "Save This Book!" button to save books that appear in search results. The button label changes to "Book Already Saved" after it is clicked and the book is saved.

A user can view their saved books on a separate page, as shown in the following animation:
![Alt text](image-2.png)

The Viewing Lernantino's Books page shows the books that the user Lernaninto has saved.

# Back-End Specifications

You’ll need to complete the following tasks in each of these back-end files:

## auth.js
- Update the auth middleware function to work with the GraphQL API.

## server.js
- Implement the Apollo Server and apply it to the Express server as middleware.

## Schemas directory

### index.js
- Export your typeDefs and resolvers.

### resolvers.js
- Define the query and mutation functionality to work with the Mongoose models.
  
  **HINT:** Use the functionality in the user-controller.js as a guide.

### typeDefs.js
- Define the necessary Query and Mutation types:

  **Query type:**
  - me: Which returns a User type.

  **Mutation type:**
  - login: Accepts an email and password as parameters; returns an Auth type.
  - addUser: Accepts a username, email, and password as parameters; returns an Auth type.
  - saveBook: Accepts a book author's array, description, title, bookId, image, and link as parameters; returns a User type. (Look into creating what's known as an input type to handle all of these parameters!)
  - removeBook: Accepts a book's bookId as a parameter; returns a User type.

**User type:**
- _id
- username
- email
- bookCount
- savedBooks (This will be an array of the Book type.)

**Book type:**
- bookId (Not the _id, but the book's id value returned from Google's Book API.)
- authors (An array of strings, as there may be more than one author.)
- description
- title
- image
- link

**Auth type:**
- token
- user (References the User type.)
  
 <br><br> 
  
# Front-End Specifications

You'll need to create the following front-end files:

## queries.js
- This will hold the query GET_ME, which will execute the me query set up using Apollo Server.

## mutations.js
- **LOGIN_USER:** Will execute the loginUser mutation set up using Apollo Server.
- **ADD_USER:** Will execute the addUser mutation.
- **SAVE_BOOK:** Will execute the saveBook mutation.
- **REMOVE_BOOK:** Will execute the removeBook mutation.

Additionally, you’ll need to complete the following tasks in each of these front-end files:

## App.jsx
- Create an Apollo Provider to make every request work with the Apollo server.

## SearchBooks.jsx
- Use the Apollo useMutation() Hook to execute the SAVE_BOOK mutation in the handleSaveBook() function instead of the saveBook() function imported from the API file.
- Make sure you keep the logic for saving the book's ID to state in the try...catch block!

## SavedBooks.jsx
- Remove the useEffect() Hook that sets the state for UserData.
- Instead, use the useQuery() Hook to execute the GET_ME query on load and save it to a variable named userData.
- Use the useMutation() Hook to execute the REMOVE_BOOK mutation in the handleDeleteBook() function instead of the deleteBook() function that's imported from the API file. (Make sure you keep the removeBookId() function in place!)

## SignupForm.jsx
- Replace the addUser() functionality imported from the API file with the ADD_USER mutation functionality.

## LoginForm.jsx
- Replace the loginUser() functionality imported from the API file with the LOGIN_USER mutation functionality.