# Note App - System Design

## Requirements

### Acceptance Criteria

* The note app runs in a client browser
* User enters a block of text
  * Save button saves the note
* User can see a list of saved notes
* User can delete a saved note

### Out of scope

* User note app account registration
* User note app account log in

### Assumptions

* The user must be logged in to use the note app
  * login is required for the user to view their saved notes
  * login is required for the user to save a new note
* the web app maintains a user session

# 1. High Level Design

1. The app will have a single page, called Notes, where all the content is displayed.
2. The list of notes will be displayed in a Sidebar at the left of the screen.
    * The sidebar will have two components: a header, and a body to display the list of notes.
    * The header will have three components: the label "Your Notes", a button to create a new note, and a button to sign out.
3. The rest of the screen will be dedicated to the informations about the selected note, this component is called NoteContent.
    * The Note content will have a header and a body.
    * The header will have an input for the note title, a button to save the note and another one to delete it.
    * The body will be an imput for the note content.
4. When the user clicks on "New" to create a new note, a temporary note will be appended to the list of notes.
5. A note will only be persisted into the database when the user hits the save button.
6. If the note is temporary and the user hits the delete button, the note will simply be removed from the rendered list of notes.

# 3. Data Model

The database system chosen for the note app is the Object-Oriented Database (OOD). 

The relevant pros are:

* Easy to save and recover data quickly, having better performance over an SQL solution.
* Easier to integrate with object-oriented programming languages such as Java.

The data model is described as follows:

```json
{
  "user": {
    "id": "string",
    "notes": [
      {
        "id": "string",
        "title": "string",
        "content": "string",
        "createdAt": "string",
        "updatedAt": "string"
      },
    ]
  }
}
```

(note that defining the exact fields for the `user` object is out of the scope of this design).

# 4. Restful API

Below are described all the required endpoints for the restful API, along with their verbs, request body, request headers, response body, and success response status. Error response statuses are out of the scope.

Get all notes
```bash
GET /notes-api/v1/{userId}/notes

Success status: 200 OK
Request headers:
  "authorization"
Request body:
  no request body
Response body:
  [Array of note objects as described in the data model]
```

Create a note
```bash
POST /notes-api/v1/{userId}/notes

Success status: 201 CREATED
Request headers:
  "content-type"
  "authorization"
Request body:
{
  "title": "string",
  "content": "string"
}
Response body:
  note object as described in the data model
```

Update a note

```bash
PUT /notes-api/v1/{userId}/notes/{noteId}

Success status: 200 OK
Request headers:
  "content-type"
  "authorization"
Request body:
{
  "title": "string",
  "content": "string"
}
Response body:
  updated note object as described in the data model
```

Delete a note
```bash
DELETE /notes-api/v1/{userId}/notes/{noteId}

Success status: 204 NO CONTENT
Request headers:
  "authorization"
Request body:
  no request body
Response body:
  no response body
```

All the above endpoints require authorization, which will be done via access token following the OAuth2 specification. However, this is out of the scope of this plan.
