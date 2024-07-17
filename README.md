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

# High Level Design

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