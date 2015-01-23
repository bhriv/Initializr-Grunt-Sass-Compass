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
	css_dir = "public/css"
	sass_dir = "public/sass"
	images_dir = "public/images"
	javascripts_dir = "public/js"
4. Ensure each of the folders listed above are setup. Manually rename and move files into correct directory if needed (i.e. rename '/javascripts/' to '/js/', manually move styles.css from '/stylesheets/' to '/public/css/')

Install Grunt
-------------

1. Follow the master (Chris Coiyer) tutorial here: http://24ways.org/2013/grunt-is-not-weird-and-hard/
2. Include the Grunt package.json file with the common dependencies. 
