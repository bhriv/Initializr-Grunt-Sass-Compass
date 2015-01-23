# Initializr-Grunt-Sass-Compass
A simple one page site to verify Grunt, Sass, Compass and Bower are all talking to one another. The directory structure uses variables within Grunt to set the output path of SASS and Compass to mimic the needs of a larger scale project.

This project requires that you have Node + NPM already installed and working. 

One Minute Install (if you have Node / NPM already installed)
------------

1. Download / Clone the repository to a new project folder.
2. Open the package.json file and give your project a name. Example: my-test-grunt
3. Open Terminal and drag and drop the new folder onto the Terminal window (or use cd /your_new_dir/ if you are comfortable with Terminal commands).
4. In Terminal type: npm install
5. In Terminal type: npm install -g grunt-cli
6. In Terminal type: grunt

That's it! You should see grunt do it's magic - concating js files, processing SASS and SCSS files using the lightning fast Libsass compiler, optimize images, build production files and put all the the assets that are ready for deployment in a /build/ folder. 

** See the references section at the bottom if you have issues.


Step-By-Step Project Setup:
------------

Manually setup new project directory including folders:

	1. #Documents (ignored local folder for any zip files or reference files)
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

1. In terminal type: compass init
2. Verify you see a config.rb file in the root directory
3. In config.rb rename the directory paths to:
	
        css_dir = "public/assets/css"
    	sass_dir = "public/assets/sass"
    	images_dir = "public/assets/images"
    	javascripts_dir = "public/assets/js"

4. Ensure each of the folders listed above are setup. Manually rename and move files into correct directory if needed (i.e. rename '/javascripts/' to '/js/', manually move styles.css from '/stylesheets/' to '/public/css/'). 

I recommend using the subfolder '/assets/' to clearly delineate the fact we are using Compass and Sass - rather than the common 'root/css' structure of Initializr or other starter frameworks. This also provides the ground to identify complex directory paths in a more involved project, such as using the Symfony framework and Assetic.

Install Grunt
-------------

Here's a condensed version of what to do once you have Node and NPM setup as per the tutorial by the master (Chris Coiyer): http://24ways.org/2013/grunt-is-not-weird-and-hard/

1. Include the Grunt package.json file (with the common dependencies) in the folder with the Compass config.rb file.
2. In terminal type: npm install
3. You should now see a /node_modules/ directory with a bunch of subdirectories (the dependency packages)
4. In terminal type: npm install -g grunt-cli
5. Copy the Gruntfile.js with the Grunt tasks we are asking Grunt to automate into the directory that contains the Compass config.rb file, and copy the test files from the /assets/ folder into your project so Grunt has some files to work on.
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

References
-------------

Grunt: http://gruntjs.com/getting-started
See http://24ways.org/2013/grunt-is-not-weird-and-hard/ for an excellent tutorial. 

Ensure npm is installed:
        npm list
    for local packages or 
        npm list -g 
    for globally installed packages.

More Info: https://www.npmjs.com/


Issues with Node + NPM
----------------

If you are like me and hit ERR's when first installing Grunt globally (-g) and trying to use Grunt then you may have a permissions issue with Node + NPM. 

You may see something like this:

        $ sudo npm install -g
        npm ERR! addLocal Could not install .
        npm ERR! Error: ENOENT, open 'package.json'
        npm ERR! If you need help, you may report this *entire* log,
        npm ERR! including the npm and node versions, at:
        npm ERR!     <http://github.com/npm/npm/issues>

        npm ERR! System Darwin 13.2.0
        npm ERR! command "node" "/usr/local/bin/npm" "install" "-g"
        npm ERR! cwd /Users/roemerbakker
        npm ERR! node -v v0.10.26
        npm ERR! npm -v 1.4.21
        npm ERR! path package.json
        npm ERR! code ENOENT
        npm ERR! errno 34
        npm ERR! 
        npm ERR! Additional logging details can be found in:
        npm ERR!     /Users/roemerbakker/npm-debug.log
        npm ERR! not ok code 0
        $ 

This was resolved by completely uninstalling Node + NPM, then fixing the folder permissions in the places that Node + NPM are installed. 

The solution was found here: http://stackoverflow.com/questions/11177954/how-do-i-completely-uninstall-node-js-and-reinstall-from-beginning-mac-os-x

To completely uninstall node + npm is to do the following:

        1.  go to /usr/local/lib and delete any node and node_modules
        2.  go to /usr/local/include and delete any node and node_modules directory
        3.  if you installed with brew install node, then run brew uninstall node in your terminal
        4.  check your Home directory for any local or lib or include folders, and delete any node ornode_modules from there
        5.  go to /usr/local/bin and delete any node executable

You may need to do the additional instructions as well:

        1.  sudo rm /usr/local/bin/npm
        2.  sudo rm /usr/local/share/man/man1/node.1
        3.  sudo rm /usr/local/lib/dtrace/node.d
        4.  sudo rm -rf ~/.npm
        5.  sudo rm -rf ~/.node-gyp
        6.  sudo rm /opt/local/bin/node
        7.  sudo rm /opt/local/include/node
        8.  sudo rm -rf /opt/local/lib/node_modules

To fix the folder permissions needed for Node + NPM to work properly follow this tutorial: https://docs.npmjs.com/getting-started/fixing-npm-permissions


