# Initializr-Grunt-Sass-Compass
A simple one page site to verify Grunt, Sass, Compass and Bower are all talking to one another. The directory structure uses variables within Grunt to set the output path of SASS and Compass to mimic the needs of a larger scale project

Project Setup:
------------

Manually setup new project directory including folders:
	1. #Documents (for any zip files or reference files)
	2. public 
	3. Z-graveyard (for files that are unused but kept for future reference)
	4. test.png (always good to a file to work with to see if this is working)


Build and Download HTML5 Initialzr Files:
------------

1. Go to: http://www.initializr.com/
2. Build a simple HTML5 starter site and download the zip to the #Documents folder.
3. Unzip the files into the /public/ folder.

Install Compass in Directory
-------------

1. In terminal type: compass install
2. Verify you see a config.rb file in the root directory
3. In config.rb rename the directory paths to:
	css_dir = "public/assets/css"
	sass_dir = "public/assets/sass"
	images_dir = "public/assets/images"
	javascripts_dir = "public/assets/js"
4. Ensure each of the folders listed above are setup. Manually rename and move files into correct directory if needed (i.e. rename '/javascripts/' to '/js/', manually move styles.css from '/stylesheets/' to '/public/css/'). I recommend using the subfolder '/assets/' to clearly delineate the fact we are using Compass and Sass - rather than the common 'root/css' structure of Initializr or other starter frameworks. This also provides the ground to identify complex directory paths in a more involved project, such as using the Symfony framework and Assetic.

Install Grunt
-------------

Here's a condensed version of what to do once you have Node and NPM setup as per the tutorial by the master (Chris Coiyer): http://24ways.org/2013/grunt-is-not-weird-and-hard/

1. Include the Grunt package.json file (with the common dependencies).
2. In terminal type: npm install
3. You should now see a /node_modules/ directory with a bunch of subdirectories (the dependency packages)
4. In terminal type: npm install -g grunt-cli
5. Copy the Gruntfile.js with the Grunt tasks we are asking Grunt to automate.
6. In terminal type: grunt
7. Watch Grunt messages and verify each Grunt task completes successfully.
8. View the Gruntfile.js and check the destination path of the css and js files.
9. Verify that Grunt put the newly created files in the expected locations. 

Example: Verify that the js has been compiled, concated outputted to the /build/ folder.
	concat: {   
        dist: {
            src: [
                '<%= dirs.js_folder %>/vendor/*.js', // All JS in the libs folder
                '<%= dirs.js_folder %>/main.js'  // This specific file
            ],
            dest: '<%= dirs.js_folder %>/build/production.js',
        }
    },

Watch Files for Changes Using Grunt
-------------

In terminal type: grunt watch
Make a change to a sass file and keep your eye on terminal. You should see the sass recompile and spit out a success message with the timestamp of the task. 

Verify JS and Sass are Working
-------------

Load the index.html file in a browser (Safari).
You should see a text shadow on the Top h1 element, and an ugly black gradient in the footer. 
The aside should have a div that reacts when hovered over.

Confirm Grunt Variables for File Locations are working
-------------

To verify we are setup correctly with full flexibility let's move the production js file to a new directory and relink. 

Since we are using the 'production-uglified.js' file in our index.html file, all we have to do is change the Uglify desination setting. We have already setup a 'dirs.build_folder' location so let's use that setting. 

1. Locate the uglify section in Gruntfile.js
2. Change the dirs.js_folder to dirs.build_folder and save the changes.

		uglify: {
            build: {
                src: '<%= dirs.js_folder %>/build/production.js',
                dest: '<%= dirs.js_folder %>/build/production-uglified.js'
            }
        },
3. In terminal type: grunt
4. Verify that you now have a '/build/' directory in your '/public/' folder containing the production-uglified.js file
5. Update the index.html file to fix the script source: <script src="build/production-uglified.js"></script>
6. BAM! You have just moved the location of your production files with a single line of code!
