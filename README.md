# CIS2750_web_forum
This web forum was developed for the CIS2750 class at the university of Guelph.  All the work is original.
---
### Description

This is a revised version of assignment 3. Instead of storing working data in a messy cluster of files, it now uses SQL to access the dursley.socs.uoguelph.ca database. That database is used for storing all user, stream, and post data that was previously found in the aforementioned collection of text files.

The db program is the largest addition to this system. It is used by the other programs (addauthor, post, view.py) as an interface for retrieving data from the database. It can also be used on its own as a command line tool to perform basic SQL queries.

__Pages__:
- home
  - allows input for username to go to dashboard page
  - button to navigate to 'add user' page
  - button to navigate to 'remove user' page
- dashboard
  options:
  - choose stream for viewing
  - make new post
- viewer
  - view messages from selected stream in selected order
- add user
  - add user to one or more streams (for multiple streams, use a comma
    separated list)
- remove user
  - remove user to one or more streams (for multiple streams, use a comma
    separated list)

---
### How to Run (db)  
  
`$ make`  
`$ ./db <flag>`  
  
__replace `<flag>` with__:  
      `-streams` : prints all stream names stores in database.  
      `-users`   : prints all usernames stored in database.  
      `-posts`   : prints all posts (messages) stored in database.  
      `-clear`   : deletes all records from every table in the database.  
      `-reset`   : drops all tables on the database.  
__Custom flags__:  
`-add <username> <streamname1> <streaname2> ...` : adds username, streamname to the 'users' table  
`-remove <username> <streamname1> <streaname2> ...` : removes username, streamname to the 'users' table 
`-post <username> <streamname> "<message>"` : adds username, streamname, message to the 'messages' table  

---
### How to Run (message-board system)

in command line, type the following:  
  `$ make`  

go to "/your/testing/folder/index.php" on the web browser of your choice  

To use a different wpml file as the first page to be loaded:  
- Go into my "Makefile".  
- Change the value of "IN" to the name of the file you would like to use.  
- Type "make" on commandline.  
  - or type make IN=your_test_file.wpml . 
- View my index.php file in your web browser.  
- The converted code from your wpml file will be displayed as a webpage.  

---
### Known Limitations

- Posts may not contain single or double quotes
- Due to the rigidity of wpml, some components of the website needed to be
  hard coded.
- When a stream is selected for viewing, every message in the stream is
  displayed.
- cannot add or remove user to/from all streams without explicitly listing the
  names of each stream in a comma separated list
- all posts in a stream are displayed at once (as opposed to one at a time)
- read count is only updated if the user clicks the "Mark all as read" button 
  (set read count to number of posts in stream being viewed) or the
  "Mark all as Unread" button (resets read count to 0).
  - Neither options work while viewing "all".

---
### Important Notes

__db__:
- I added 3 other cmd arg flags that are used by post & addauthor.
  -add
  -remove
  -post

__config_parser__:
- It is expected that:
  - every quptation mark will have a corresponding end quote
  - every open bracket has a corresponding closing bracket
  - closing quotes & closing brackets are found on the same line as their
    counterparts
  - a string literal will not contain a string literal within it
- Anything inside the brackets of an element that is not a defined property &
  is not a comma is passed through the parser verbatim
- The location of insertion of the extra content (if any is found) is dependent
  on which element tag it belongs to
  .d -- extra content added after <hr /> tag
  .b -- extra content added inside form between submit button & </form> tag
  .e -- extra content added after execution before the ?> php closing tag
  .h -- extra content added after text & before header closing tag
  .i -- extra content added after last input field, before 'submit' input tag
  .l -- extra content added inside link tag: <a ... HERE ... href=...>text</a>
  .p -- extra content added in same relative location as link tag
  .r -- extra content added between last radio button & submit button
  .t -- extra content added outside of (after) the <p> ... </p> paragraph tags

---
