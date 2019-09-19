# Journal
An informal log of the Makerspace journey of discovery
## Index
#### Get Started with the Makerspace Journal
[Get Started with the Journal](#get-started-with-the-journal)

#### AWS
[upload/download using CLI](https://github.com/usgs-makerspace/wbeep-viz#get-the-map-tiles-and-add-them-to-the-project)

#### Font Awesome 
[Use Font Awesome with Vue](https://github.com/usgs-makerspace/wbeep-viz#add-font-awesome-icons-1)

#### Leaflet
[Leaflet Example Using Vue and Vue2Leaflet Plugin](https://github.com/usgs-makerspace/makerspace-vue2leaflet-example#testing-area-for-wbeep)

#### MButils 
[How to unpack .mtiles files to .pbf](#mbutil)

#### Water Budget and Estimation and Evaluation Project (WBEEP)
[Project Setup](https://github.com/usgs-makerspace/wbeep-viz#project-setup-1)

[Automated Builds](https://github.com/usgs-makerspace/wbeep-viz#automated-builds-1)

[Working Base Tile Layers](#working-base-tile-layers)

#### United States Web Design System (USWDS)
[Vue Example Using USWD and USGS Headers and Footers](https://github.com/usgs-makerspace/makerspace-vue2leaflet-example#testing-area-for-wbeep)

#### Vue
[Vue Example Using USWD and USGS Headers and Footers](https://github.com/usgs-makerspace/makerspace-vue2leaflet-example#testing-area-for-wbeep)

#### Mapbox gl js
[How to Overzoom in Mapbox](#tile-layers-overzoom)

[Background Black in Fullscreen mode](#background-black-in-fullscreen-mode)

***
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
##### MBUtil
Just as note, OpenMapTiles downloads come as a single '.mbtiles' file. Since we need the tiles to be in '.pbf' form to use on S3 we needed to open the '.mbtiles' file in some way. At first we attempted to convert the file to GeoJSON using the 'Tippecanoe' (https://github.com/mapbox/tippecanoe) program and this command, tippecanoe-decode yourmbtilesfile.mbtiles > yourjsonfile.json . This worked fairly well. The original '.mbtiles' for the United States OpenStreetMap vector tiles was about 7.2GB. The conversion to GeoJSON took about two hours and resulted in a file approximately 75GB. However we were stymied when attempting to convert the GeoJSON to the required '.pbf' format. The Tippecanoe command tippecanoe -e diretoryYouWantTheFilesIn/ -Z 3 -z 10 yourgeojsonfile.json seemed as if it would work. However, running this command seemed to invoke a process that may have run for several days as well as taking up all available hard drive space.

Rather than continue down a path that seemed doomed. We switched direction and found a program called MBUTIL (https://github.com/mapbox/mbutil). Using MBUTIL we were able to export the 7.5GB '.mbtiles' file to a directory of '.pbf' file with this command, mb-util world.mbtiles tiles (note the word 'tiles' denotes the name of a directory that must NOT already exist. MBUTIL was able to 'explode' the '.mbtiles' file to '.pbf's in less than 40 minutes.
``` 
A generalized example of using MBUTIL
mb-util yourtiles.mbtiles targetDirectory 
// note the 'targetDirectory' directory must not already exist 
// and this example also assumes the command is run from the directory containing the '.mbtiles' file.

Here is an specific example
mb-util openmaptiles_us.mbtiles pbf

```
Once we had the correct format, we attempted to upload them to S3. This proved to be a huge pain in the hinder, due to network issues and the large file size (75GB+). What did prove to be a saving grace was the use of the AWS CLI 'sync' command. This command wastes time for normal copy procedures where 'cp' is the more applicable choice. However, in this case, it was a life saver since the 'sync' command allows you to pick up where you left off after you have been disconnected do to VPN or other issues. Since 'sync' compares what we want to upload to want is already in the destination there is an initial delay in the process while AWS CLI processes the differences (with files loads this size, the compare was taking up to 15 minutes), However the payback is that you can recover from issues that interrupt the upload without having to start over.

This is an example of the correct commands
```
Loading all of the current working directory to S3:
aws s3 sync . s3://wbeep-test-website/openmaptiles/ --content-encoding 'gzip' --content-type 'application/x-protobuf'

Loading a specific directory
 - loading files from 14th zoom level locally, to 14 zoom level on S3:
aws s3 sync ./14 s3://wbeep-test-website/openmaptiles/14/ --content-encoding 'gzip' --content-type 'application/x-protobuf'.
```

### Background Black in Fullscreen mode
Just a quick note, when styling a map for use with Mapbox gl we ran into this problem, the background appeared as intended 
when in the standard mode, but when switching to 'fullscreen' the background turned black. We are not sure of the internal Mapbox
gl reasons for this, however the cause was the use of an 'alpha' channel on the background. This issue will occur whether 
you use 'rgba' or 'hsla' for the  color definition. The weird part of this issue is not that the background appears black while
in  'fullscreen' mode but that it acts correctly in the normal mode. Additionally, if a background color is not set, any color
fills using an alpha channel will also turn black upon entering 'fullscreen' mode.
```
To avoid the black background follow these steps
1 - always set a backgound color
2 - always use and color definition without an 'alpha' channel for the background - example rgb(0, 0, 0)

note - If you set the background color as stated above, you will have no issues with using colors with 'alpha' channels 
with other layer color fills. If not, well . . . who knows what evils will result
```


### Tile Layers Overzoom
'Overzoom' is a feature of Mapbox gl that allows it to make an educated 'guess' and display a map layer for tiles that
don't really exist in the tile set. This works for both raster and vector tiles. However, a nice feature of vector 
map tiles is that the ability to zoom in past the 'real' zoom level only slightly reduces image quality -- loss in quality is greater for raster tiles. 
Yet, even with vector tiles 'overzoom' creates some loss of precision, so good judgment should be used in situations where 
the exactness of the map is paramount. 
However, in many situations having a mapping library such as Mapbox gl js mathematically extend zooms levels is an 
acceptable option. To get this to work you need to keep a few things in mind.

Mapbox gl js sets the map zoom level extents in three different places
```
1) Where the map is created
2) Where the source is declared
3) Where the layer is defined
```
Let's talk about these separately. First, when the map is created we can set a pair of zoom level parameters.
```
Here is an example of setting map creation parameters in an application using the Vue framework and Vue components. This 
code would be located in the 'script' section.
        },
        data() {
            return {
                mapStyle: mapStyles.style,
                container: 'map',
                zoom: 3,
                minZoom: 3,
                maxZoom: 23,
                center: [-75.072994, 40.544454],
                pitch: 0, // tips the map from 0 to 60 degrees
                bearing: 0, // starting rotation of the map from 0 to 360
                hoveredHRUId: null,
                legendTitle: 'Legend'
            }
        },
```
Setting the 'minZoom' (note the term 'minZoom' is not the 'official' Mapbox term, which is 'minzoom' (all one word, all lower case), 
I can't really get into a full explanation of why this now, other than to say it is a Vue framework related thing, so just pretend that the term used is 'minzoom',
and we will move on). Notice that the minimum and maximum here are 3, and 23. The complete range of zoom levels of
which Mapbox gl is capable of rendering is 0 to 23. The setting of 0 represents the entire world (mercator projection) in 
view port (the area of the screen in which the map is allowed to show), while 23 represents an extremely zoomed in version.
A internet search of 'mapbox zoom levels' will give you a full explanation of the topic. 

What the above code does is set the 'hard stops' of the map. The map will not zoom out past zoom level 3 (which is just a bit bigger than the size of the continental US) nor will it
zoom in past level 23. Of course, level 23 is the limit that Mapbox gl can display, so that line could be omitted without a 
change in application behavior, however for completeness will leave it in.  

So far this all seems straight forward and sensible, however the next steps required to tell Mapbox gl to overzoom are 
not totally intuitive. As mentioned above, there are three places in which we tell Mapbox gl how to control zoom levels.
The second one mentioned, 'Where the source is declared', is critical to getting the overzoom to function. 
```
// This is a snippet from the Mapbox style sheet (in our application it is usually /src/assets/mapStyles/mapStyles.js)
 sources: {
    openmaptiles: {
        type: 'vector',
        'tiles': ['http://wbeep-test-website.s3-website-us-west-2.amazonaws.com/openmaptiles/{z}/{x}/{y}.pbf'],
        "minzoom": 0,
        "maxzoom": 14
    },
```
It is important to note that the 'minzoom' and 'maxzoom' are not required parameters. Leaving them out will cause the map
to default to real tile extents. The main advantage of setting these parameters to the high and low end zoom levels of your 
tile set is that Mapbox gl will not attempt to look for any source layers outside of this range. This saves many wasted 
web calls for resources that don't exist. 
```
Important stuff about setting the zoom level parameters in the source
1)  If you do not specify a minimum or maximum zoom, your map layer for that tile will go blank. 
        when you zoom past the limit of your tile set
2) If you set the limits past the extents of your tile set, there are no ill effects, however your map layer for
        that tile will go blank just as mentioned above.  
3) If you set the 'minzoom' limit inside your tile extent, the any tile above that zoom will appear be blank.
4) If you set the 'maxzoom' limit inside your tile extent, Mapbox gl will stop loading the real tiles and will 
        'overzoom' the remaining zoom levels to the limit you set in the first step of the section,
        back when the map was created.
5) If you set the 'maxzoom' limit to the match the limit of your tile set, Mapbox gl will begin to overzoom
        when the zoom level reachs the actual level of your tiles.
6) IMPORTANT - If you set the 'maxzoom' greater than the extent of your actual tileset,
     'overzoom' will NOT work.
```

The moral of the above is that if you want Mapbox gl to 'overzoom' your tiles you must set the 'maxzoom' in source declaration
to less than or equal to your actual set extent.

Now this brings us to the third place where the zoom extents in the are defined, and that is at the layer level. So far
we have discussed how to control the zoom levels of the entire map (at map creation), of the entire source (when we
define the tile source), and now we will describe the zoom extents at the layer level and how that relates to 'overzoom'.
After the 'sources' are defined in the Mapbox style sheet the different layers are styles. Each vector tile 'source' can contain
many 'layers', and each of those can be given 'minzoom' and 'maxzoom' extents. 
```
Example of a 'layer' defined in the Mapbox gl style sheet
            {
                'filter': ['all', ['==', '$type', 'LineString'],
                    ['!in', 'brunnel', 'tunnel', 'bridge'],
                    ['==', 'intermittent', 1]
                ],
                'id': 'waterway_intermittent',
                'paint': {
                    'line-color': 'hsl(205, 56%, 73%)',
                    'line-opacity': 1,
                    'line-width': {
                        'base': 1.4,
                        'stops': [
                            [8, 1],
                            [20, 8]
                        ]
                    },
                    'line-dasharray': [2, 1]
                },
                'minzoom': 3,  // here are the settings we have an interest in 
                'maxzoom': 23,
                'source': 'openmaptiles',
                'source-layer': 'waterway',
                'type': 'line',
                'layout': {
                    'visibility': 'visible'
                },
                'showButton': false,
                'inLegend' : false
            },
```
Just as with the map, and the source definitions, the each layer does not require you to set the 'maxzoom' or the 'minzoom'.
However, setting these will give you control as to the zoom level a particular layer will first appear. For example,
having a 'minzoom' set to 3, as above, in conjunction with the map and source settings, will cause the layer to show
as soon as the map appears. This is because map has a 'minzoom' of 3, which is the same as the layer. If we set the 
layer 'minzoom' to 8, for example, the user would have to zoom in five levels before the layer will show.

To make the 'overzoom' work for any given layer, we must set the layer 'maxzoom' to greater than the 'maxzoom' of the
source (and obviously the map). We also must have the source 'maxzoom' set to less than or equal to the real zoom levels
available in the tile set. 

To sum up, if you want to 'overzoom', you must 1) let the map allow it by setting the 'maxzoom' to a number greater than
your real tile set extent, 2) set the source 'maxzoom' definition to less than or equal to the real tile extent, and 3) set the 
layer definition to greater than the source definition but less or equal to the map 'maxzoom'. 