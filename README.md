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
5. Copy the Gruntfile.js with the Grunt tasks we are specifying


