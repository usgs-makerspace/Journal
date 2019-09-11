# Journal
An informal log of the Makerspace journey of discovery
## Index
#### Get Started with the Makerspace Journal
[Get Started with the Journal](#get-started-with-the-journal)
[Working Base Tile Layers](#working-base-tile-layers)
#### Water Budget and Estimation and Evaluation Project (WBEEP)
[Project Setup](https://github.com/usgs-makerspace/wbeep-viz#project-setup-1)
[Automated Builds](https://github.com/usgs-makerspace/wbeep-viz#automated-builds-1)

#### Font Awesome 
[Use Font Awesome with Vue](https://github.com/usgs-makerspace/wbeep-viz#add-font-awesome-icons-1)

#### Leaflet
[Leaflet Example Using Vue and Vue2Leaflet Plugin](https://github.com/usgs-makerspace/makerspace-vue2leaflet-example#testing-area-for-wbeep)

#### Vue
[Vue Example Using USWD and USGS Headers and Footers](https://github.com/usgs-makerspace/makerspace-vue2leaflet-example#testing-area-for-wbeep)

#### United States Web Design System (USWDS)
[Vue Example Using USWD and USGS Headers and Footers](https://github.com/usgs-makerspace/makerspace-vue2leaflet-example#testing-area-for-wbeep)




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

### Working Base Tile Layers
Makerspace has been on a quest to get base tile layers that we can use with our maps. We tried many different options. 
Including some internal USGS sources. None of these panned out. For a short time we had hope that we could use tiles served from
Mapbox as long as we stayed inside of the 'free tier', but we were later told that if it required use of an access token (and all Mapbox services require a token)
than we could not use it , as Mapbox would then be acting as a 'cloud resource' which falls in the purview of CHS (Cloud Hosting
Solutions) and would require their official sanction, which they have not given. We also tested a number of free layers, including
those from http://maps.stamen.com, but they all had limitations (however http://maps.stamen.com, does have some very interesting
layer style examples that may be of use at some point).
 
In the end we decided to use OpenMapTiles. OpenMapTiles provides a base layer (with streets, waterways, etc) that is free to use in 
open source projects provided an 'attribution' is added to the map.

Just as note, OpenMapTiles downloads come as a single '.mbtiles' file. Since we need the tiles to be in '.pbf' form to use on S3 we needed to open the '.mbtiles' file in some way. At first we attempted to convert the file to GeoJSON using the 'Tippecanoe' (https://github.com/mapbox/tippecanoe) program and this command, tippecanoe-decode yourmbtilesfile.mbtiles > yourjsonfile.json . This worked fairly well. The original '.mbtiles' for the United States OpenStreetMap vector tiles was about 7.2GB. The conversion to GeoJSON took about two hours and resulted in a file approximately 75GB. However we were stymied when attempting to convert the GeoJSON to the required '.pbf' format. The Tippecanoe command tippecanoe -e diretoryYouWantTheFilesIn/ -Z 3 -z 10 yourgeojsonfile.json seemed as if it would work. However, running this command seemed to invoke a process that may have run for several days as well as taking up all available hard drive space.

Rather than continue down a path that seemed doomed. We switched direction and found a program called MBUTIL (https://github.com/mapbox/mbutil). Using MBUTIL we were able to export the 7.5GB '.mbtiles' file to a directory of '.pbf' file with this command, mb-util world.mbtiles tiles (note the word 'tiles' denotes the name of a directory that must NOT already exist. MBUTIL was able to 'explode' the '.mbtiles' file to '.pbf's in less than 40 minutes.

Once we had the correct format, we attempted to upload them to S3. This proved to be a huge pain in the hinder, due to network issues and the large file size (75GB+). What did prove to be a saving grace was the use of the AWS CLI 'sync' command. This command wastes time for normal copy procedures where 'cp' is the more applicable choice. However, in this case, it was a life saver since the 'sync' command allows you to pick up where you left off after you have been disconnected do to VPN or other issues. Since 'sync' compares what we want to upload to want is already in the destination there is an initial delay in the process while AWS CLI processes the differences (with files loads this size, the compare was taking up to 15 minutes), However the payback is that you can recover from issues that interrupt the upload without having to start over.

This is an example of the correct commands
```
Loading all of the current working directory to S3:
aws s3 sync . s3://wbeep-test-website/openmaptiles/ --content-encoding 'gzip' --content-type 'application/x-protobuf'

Loading a specific directory
 - loading files from 14th zoom level locally, to 14 zoom level on S3:
aws s3 sync ./14 s3://wbeep-test-website/openmaptiles/14/ --content-encoding 'gzip' --content-type 'application/x-protobuf'.
```
So we now have set of United States 'streets' vector tiles (levels 0-14) hosted on 'test'.

We still need to figure out how we should deploy this to the tiers (keeping in mind that this process took about 5 days)

