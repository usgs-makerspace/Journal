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

Once you make your heading, copy it and immediately (otherwise you will forget; be honest with yourself, you know that you will) 
hit the 'control' and 'home' keys at the same time to return to the top of the page. Once there, follow the pattern to 
add your header to the Journal's index. 
```
A basic summary of the link pattern
Put the words you want people to see when the page is displayed on in square brackets '[your link name here]'
Follow that (leaving no space) with a pair of parentheses filed with your header name.
  '(#your-header-name)' 
Here are the confusing parts
1 - No matter how many '#' your actual header has, it will only have one '#' in the link. 
2 - There is no space between the '#' and the link name.
3 - Your link name must be in all lower case
4 - Your link must have all the spaces replaced with dashes (the minus sign '-').
5 - Why is this? I have no idea, but if you miss any of the above, your link will not work.
Note: You can also link to any valid URL (like other Github repositories) by placing the URL in the parentheses.
Example: [title](https://www.example.com) 
```  

Awesome, you should now have a link in the index to your Journal entry. Jump back down and fill in the content. For the most part,
you can just just and paste text then add a bit of formatting. For a guide on Markdown forwarding,
try and internet search for 'markdown cheat sheet'. You should find may great examples.
#### What makes a good Journal entry?
1 - Did you just complete a task that seemed simple at first but turned out to have a bunch of pit falls and traps that made completeing it a 
huge pain in the arse? If so, save your fellow team members the pain of having to learn those hard lessons all over again
and add your knowledge here. Your teammates will thank you.

2 -  Did you do a research task? If so, the world wants to know your results. To document research tasks follow this pattern (currently in beta, 
please feel free to improve the pattern) 
```
Research Task Check List
1 - State when you did the task
2 - State why you did the task
3 - State what you did
4 - State your conclusion/results/recommendations 
```
#### Inserting images
The big downside to using markdown for a journal is that adding images require more than cutting and pasting - boo.
To  get an image into the Journal first add the image to the project in the folder called 'markDownImages'.
Then add a link to the image you want displayed using the following pattern.
```
// A general example for adding an image link.
![alt text](image.jpg)

// A specific example . . .
![screen shot of WBEEP UI](./markDownImages/wbeepSample.png)
```

Here is the above link in action.
![screen shot of WBEEP UI](./markDownImages/wbeepSample.png)

#### Summary
Now you have the basic idea of how to add entries to the Journal. Have fun and good luck.
