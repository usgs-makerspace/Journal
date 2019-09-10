# Journal
An informal log of the Makerspace journey of discovery
## Index
[Get Started with the Journal](#get-started-with-the-journal)

### Get Started with the Journal
To start adding to the Makerspace Journal, the first thing you need to do is 'fork' the repository. Then clone your fork
to your local machine and set the canonical master branch as a remote connection named 'upstream'. 

This is the basic code.
```
Assuming you have 'forked' the 'Journal' repository . . .
git clone https://github.com/<yourUserName>/Journal.git
cd Journal
git remote -v 
// The line above will list the connection to the remote git repository
// This should be your fork. It will be called 'origin' and have a 'push' and 'fetch' associated with it.
git remote add upstream https://github.com/usgs-makerspace/Journal.git 
// The above line will create a remote connection that you have named 'upstream'.  
// This is a connection to the canonical repository and will let you pull the newest code from there.
git remote -v
// The line above should now have four connections, two called 'origin' and two called 'upstream'
```

With the basics out of the way, you are ready to start you first journal entry. In a code editor with the capacity to edit
'Markdown' files ('.md'), open the README.md. If your code editor stinks at editing 'Markdown' files there are many online 
editors available. Just do a search for 'online markdown editor' and you will find something that will work for you. You
can edit you journal entry there, and paste it back into the code.

Step 1 -  Hit the 'control' and 'end' keys simultaneously to jump to the end of the document and create a heading, such as '### 
My New Heading'. The '#' number signs (hash tags, for you Twitter fans) indicates that what you write after it will be a
heading, with one number sign marking your primary header and additional number signs indicated a progression of declining precedence.

Once you make your heading copy it and immediately (otherwise you will forget; be honest with yourself, you know that you will) 
hit the 'control' and 'home' keys at the same time to return to the top of the page. Once there follow the pattern to 
add your header to the Journal's index.  