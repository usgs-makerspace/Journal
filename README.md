# Journal
An informal log of the Makerspace journey of discovery
## Index
#### Get Started with the Makerspace Journal
[Get Started with the Journal](#get-started-with-the-journal)

#### AWS
[upload/download using CLI](https://github.com/usgs-makerspace/wbeep-viz#get-the-map-tiles-and-add-them-to-the-project)

#### Font Awesome 
[Use Font Awesome with Vue](https://github.com/usgs-makerspace/wbeep-viz#add-font-awesome-icons-1)

[Using Facebook/Twitter Icons with Vue](https://github.com/usgs-makerspace/wbeep-viz#using-facebook-and-twitter-icons-with-vue)

[Font Awesome (secret) styling](https://github.com/usgs-makerspace/wbeep-viz#fontawesome-icon-secret-styling)
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
[Vue Environment Variables and the build](#vue-enviroment-variables)

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
                maxZoom: 24,
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
and we will move on). Notice that the minimum and maximum here are 3, and 24. The complete range of zoom levels of
which Mapbox gl is capable of rendering is 0 to 24. The setting of 0 represents the entire world (mercator projection) in 
view port (the area of the screen in which the map is allowed to show), while 24 represents an extremely zoomed in version.
A internet search of 'mapbox zoom levels' will give you a full explanation of the topic. 

What the above code does is set the 'hard stops' of the map. The map will not zoom out past zoom level 3 (which is just a bit bigger than the size of the continental US) nor will it
zoom in past level 24. Of course, level 24 is the limit that Mapbox gl can display, so that line could be omitted without a 
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
3) If you set the 'minzoom' limit inside your tile extent, any tile above that zoom will appear be blank.
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
After the 'sources' are defined in the Mapbox style sheet the different layers are styled. Each vector tile 'source' can contain
many 'layers', and each of those can be given 'minzoom' and 'maxzoom' parameters. 
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
                'maxzoom': 24,
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
Just as with the map and the source definitions, layer definitions do not require you to set the 'maxzoom' or the 'minzoom'.
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

### Vue Environment Variables
Vue has a slick, built-in way of handling environment variables, however there are a few gotchas and important points to know
before diving in.

Background information . . .

Vue has build modes (think environments). Some of those build modes are defaults, others can be created to meet custom needs. When you create
a new Vue project it will have a few default build modes set up (dependent on the choices you made during setup). You can see these modes in the 'package.json'.
```
Here is a snippet from a generic 'package.json' in a Vue project. 
Notice the 'scripts' section.
. . . 
{
  "name": "generic project",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "serve": "vue-cli-service serve",
    "build-test": "vue-cli-service build",
    "lint": "vue-cli-service lint"
  },
  "dependencies": { . . .
```
In the 'scripts' section of the 'package.json', we see some 'key/value pairs', such as "serve": "vue-cli-service serve" 
(where 'serve' is the key and 'vue-cli-service serve' is the value). Since we are using Node Package Manager (NPM) for 
package management, the keys are NPM short cuts for the values. If you have done some of our Vue tutorials, such as 
[Leaflet Example Using Vue and Vue2Leaflet Plugin](https://github.com/usgs-makerspace/makerspace-vue2leaflet-example#testing-area-for-wbeep), 
you may remember that to start the Vue Development Server and view our project on localhost, we ran 'npm run serve'. In this
case we are telling NPM to 'run' the command 'serve' which we have tied to the Vue CLI (Command Line Interface) command, 'vue-cli-service serve'.
Running either 'vue-cli-service serve' or 'npm run serve' will give you the same result, PROVIDED you have Vue CLI installed either in your 
current working directory or as a globally accessible module in your operating system (otherwise you will get the error 'vue-cli-service: command not found
'). The NPM in your project has access to the Vue CLI commands in your project, which is why it can run them without you 
explicitly installing Vue CLI.

The important thing to remember here is that the default scripts you see above are linked by default to certain Vue build
environments, those environments being 'development', 'test', 'production'.
```
    'development' is used by vue-cli-service serve
    'test' is used by vue-cli-service test:unit
    'production' is used by vue-cli-service build and vue-cli-service test:e2e
```
This means that when we run 'npm run serve' Vue will look for any environment variables we have set up in the environment called 'development.


Let's pause here for a second and talk about NODE_ENV. NODE_ENV is a Vue variable that is always active in Vue and it stores information about the Vue environment in which we
are running. If you add 'console.log('node-env ', process.env.NODE_ENV)' to your code, you can see what environment is active.

Looking at the log statement above you will see 'process.env.' prior to the name of the  NODE_ENV variable, this is how 
we connect to environment variables (at least in JavaScript code, in HTML things are a bit different, and we'll talk about that
later).

Let's take a look at one more thing before we move on
to setting up some  variables. As I mentioned earlier, when Vue receives the serve/build command from NPM it will, by default,
use a certain set of environment variables. What variables are used are determined by the 'mode' in which Vue is running.
The 'mode' is basically the same thing as the 'environment' (not exactly, but for our purposes it is close enough). Also,
as mentioned earlier, there are three default modes 'development','production','test'. 

#### Running a Vue Project with Vue Environment Variables
##### Vue Builds and Vue Build Modes are Different!!
It is important to note that modes are NOT the same as builds. By default, Vue has three types of builds, development, 
production and test.  This is very confusing since the names are the same as some of the modes, but rest assured that they are
quite different. When we run 'npm run serve' we are doing a 'development' build using the mode 'development'. As I will 
discuss later we can do a 'development' build with a 'production' mode. 

Without getting into to much detail, 'npm run serve' runs a development build which is a build for local development. The 
code is not fully bundled, minimized, or sent to the 'dist' folder for deployment. Instead the code is optimized to run 
locally using the Vue Development Server, along with Webpack's Hot Module Swap capabilities. 

Running 'npm run build' runs a production build which minimizes and bundles the application to the 'dist' directory, making it
ready for future deployment.

Running 'npm run test' runs a build optimized to run various code tests.

The modes are a totally separate concept from builds. The modes tell Vue which set of environment variables to use. So we
can actually specify both the build and mode by adding '-- mode modeType' to end of our npm run command.
```
Example of add a 'mode' flag
 'npm run serve --mode development'.
``` 

 
You may have realized, from what was said previously, that there is no functional difference between 'npm run serve --mode development'
and 'npm run serve' since the default mode for 'npm run serve' is development. However, if we would like to we can do something 
like 'npm run serve --mode production' which will tell Vue to do a development build (set up for local development) and
but load all the 'production' environment variables. This is very helpful if you want to see the 'production' version of the 
application locally. 

Finally we now have the basic understanding needed to use Vue environment variables effectively. To create variables that
Vue can use we will need to add a file or two to the root directory of our project. The basic file for Vue environment variables
is '.env'. Variables in the '.env' file are loaded in all modes. The values are entered in format 'key=value'. 
```
Notes for Enviorment Variables
1) format is key=value , for example VUE_APP_TITLE=National Integrated Water Availability Assessments
2) ALL VALUES ARE STRINGS! (so there are no booleans or numbers)
3) You can use booleans or numbers, but they will be strings. 
    For example APP_VUE_IS_BORKED=true will work, but true will be a string, not a boolean (same for number values)
4) Don't leave a space between the key and the equals sign or the value and the equals sign
5) You don't need quotes around your strings, and beware of white space at the end
6) You can make comments using the '#' symbol, such as # this is a comment
```
Here is an example file . . .
```
VUE_APP_TITLE=National Integrated Water Availability Assessments
VUE_APP_TIER=DEV

# Controls the feature toggle for having the map zoom level show at the bottom of the page
VUE_APP_ADD_ZOOM_LEVEL_DISPLAY=true

# The URL for the Hydrological Response Unit tiles
VUE_APP_HRU_TILE_URL=http://wbeep-test-website.s3-website-us-west-2.amazonaws.com/tiles/{z}/{x}/{y}.pbf?fresh=true

# The URL for the file that gives us the date of the model data
VUE_APP_DATA_DATE_URL=https://wbeep-test-website.s3-us-west-2.amazonaws.com/date/date.txt
```

Now that we have the basic idea, the using the magic of environment variables is fairly straight forward. If we 
want a set of variables available to a particular build we must do three things.
```
Remember to use your variables you must
1) create a .env file with the correct name such as .env.production
2) add your variables to that file (as described above)
3) run the build with the correct mode
    for example 'npm run serve --mode production'
```

To make running our project easier to run (and easier for other developers to understand) we can add custom builds
to our 'package.json'. If you remember from earlier, our generic 'package.json' looked like  . . .
```
. . . 
{
  "name": "generic project",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "serve": "vue-cli-service serve",
    "build-test": "vue-cli-service build",
    "lint": "vue-cli-service lint"
  },
  "dependencies": { . . .
```
We can customize this by adding more specific commands to the 'scripts' section.

```
  "private": true,
  "scripts": {
    "serve": "vue-cli-service serve --mode development", // this is the standard local dev build (same as "serve": "vue-cli-service serve")
    "serve-prod": "vue-cli-service serve --mode production", // this lets us do a local dev build running the 'production' environment variables
    "build-test": "vue-cli-service build --mode development", // a production build, using the 'development' environment variables (for deployment to our 'test' tier
    "build": "vue-cli-service build --mode production", // a production build, using the 'production' environment variables for deployment to our 'production' tier
    "lint": "vue-cli-service lint"
  },
  "dependencies": {
```
With the above changes added to the 'package.json' file we can run a command such as 'npm run serve-prod'. This NPM shortcut
will run the Vue CLI command 'vue-cli-service serve --mode production' which will build a version of our application to run on
the Vue Development Server that has all our the production variables. In other words this is how to run the production 
version of the application locally.

#### Hints on Using Vue Environment Variables
Once you have an understanding of background concepts, actually using the variables is pretty simple. Here are just a few
hints to help you along the way.
```
1) Restart your development server to have new environment variables 
        added to the application (yes, this one will trip you up at some point)
2) Prefix all your variables with 'APP_VUE_' 
        so that webpack knows to embed the varibles in the code
3) Use 'process.env.', in a JavaScript section of the code, to grab the value of the variable
    Generic example - 'process.env.APP_VUE_VARIABLE_NAME'
    Specific example - 'console.log('node-env ', process.env.NODE_ENV)'
4) Use '<%= VUE_APP_VARIABLE_NAME %>' to access the variable vaule in HTML code
    Specific example - '<title><%= VUE_APP_TIER %><%= VUE_APP_TITLE %></title>'
```


```
Summary of helpful Vue environment variable commands

// Get the value of variable in JavaScript code
process.env.VUE_APP_YOUR_VARIABLE_NAME

// Confirm the environment your are in
console.log('node-env, this is the curent environment: ', process.env.NODE_ENV)

// See a list of all the enviorment variables
console.log('A list of all the current environment variables: ',  process.env)

```


  
