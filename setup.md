Things you'll need:<br/>
<strong>node/npm</strong> : <a href="https://nodejs.org/en/download/">https://nodejs.org/en/download/</a><br/>
<strong>git</strong> : <a href="https://git-for-windows.github.io/">https://git-for-windows.github.io/</a><br/>
<strong>your favorite code editor</strong> I suggest Sublime : <a href="http://www.sublimetext.com/2">http://www.sublimetext.com/2</a><br/>
<strong>Ruby</strong> : <a href="http://rubyinstaller.org/downloads/">http://rubyinstaller.org/downloads/</a> We're going to need this for Sass - our CSS preprocessor which lets us use variables and stuff in our CSS. 

Once you have Node installed, you'll also have 'npm' which is 'node package manager'. It lets you install all kinds of stuff that people have created for node. One of those things that someone made is called <a href="http://yeoman.io/learning/index.html">Yeoman</a>. It's a tool that generates the scaffolding for all kinds of different webapps. It helps you so that you don't have to install all of the peices you need for a web app one by one and it sets it all up for you. 

Let's install it and its dependancies. Open up a command prompt (we'll do a lot from command prompt so hopefully you're used to using it) and copy paste this:
<code>npm install -g yo bower grunt grunt-cli gulp</code>

the -g flag means install it globally. This allows you to use the packages you're installing from anywhere on your command line. Without it, it will only install it locally within your current directory and you'll only be able to use from in here. Some things need to be installed globally and others locally. You'll figure this out as you go and ill tell you which to do for now. 

"yo" is short for Yeoman, which is our web app generator.<br/>
"bower" is another package manager. It's similar to npm, but the difference is in how they manage their dependancies. Both are useful.<br/>
"grunt", "grunt-cli", and "gulp" are task managers. These are used to "build" your javascript/css and a bunch of other automated tasks. It's really just Grunt and Gulp, but the grunt-cli gives you a command line interface. 

We're going to use <a href="http://expressjs.com/en/index.html">Express</a> which is a framework for Node apps. NPM lets us install a yeoman generator for Express that someone already built for us. Copy and paste this in your console:

<code>npm install -g generator-express</code>

Once that has installed, then we will make a new express app (make sure you're in the folder you want set this up in):

<code>yo express</code>

This will walk you through a couple questions on start up. Use your up/down arrow keys to navigate the choices and press enter to make selections.

The first thing it will ask you if is if you want to create a new directory for your project. Since you should already be in the folder you want, you can type "n" for no. Otherwise it will create a new folder inside the directory you're already in.<br/>
Next you have the choice between Basic and MVC (model/View/Controller). Let's go with Basic for this project.<br/>
Next it gives you options for templating language. We'll choose Handlebars, but feel free to look up the others. Handlebars is very similar to Mustache (which is what i was showing you before), so we'll go with that one. Some of the others are bizaare and I hate working with them. <br/>
Next is the css-preprocessor. Choose Sass. (you should have installed Ruby earlier, Sass requires it).<br/>
Last is the task manager. Choose Grunt.

It will then go through the rest of the install process. Once it has completed, we'll take a look at what it installed. 

Your directory structure should look like this:

<strong>app.js</strong> - This is part of Express. <br/>
<strong>bin</strong> - This contains your www file. It's what configures your node server.  <br/>
<strong>bower.json</strong> - a configuration file for Bower dependancies. You wont need to do anything with this. <br/>
<strong>Gruntfile.js</strong> - your configuration for Grunt tasks. You wont need to do anything here for now, but maybe eventually we can dig into this more later.
<strong>node_modules</strong> This is where everything that gets installed via "npm install" will get put. These are defined in your package.json file<br/>
<strong>package.json</strong> This is the main configuration for npm dependancies for your app. When you start building Node apps, this is where you will define all of its dependancies. Anytime you see a project that has a package.json file, running <code>npm install</code> from the same directory as the package.json file will examine the file and install all of the packages that the app needs to run. This essentially makes your app portable. You can build something and define all of the packages that you used here. Then you can host it online or send it to someone and they just need to run "npm install" to get all of your apps dependancies. <br/>
<strong>public</strong> - part of Express. This is where all of your static assets go (js, css, images, etc) <br/>
<strong>routes</strong> - part of Express. This is where you define all of your endpoints. 
<strong>views</strong> - part of Express. This is where your views live that get served up by your endpoints. You'll notice that these are all Handlebars templetes since thats what we chose from our Yeoman generator. It's essentially HTML markup, with placeholders for variables. 

If you open up routes/index.js, you'll see this code:

<code>
router.get('/', function(req, res) {
  res.render('index', { title: 'Express' });
});
</code>

This defines what to do when someone hits the root of your app ("/"). res.render renders your response (res) and it takes two arguments. The first is the template name ('index'), and the second is just an object {title: 'Express'}

If you open up views/index.handlebars (which is the template name we told our response to serve), you can see exactly how it works. The object we passed to it has a property called "title", and that title property is being replaced in the template with what we set it as ('Express'). So everywhere you see {{title}} in the template will get replaced with 'Express'. 

So now if we go back to our command line, (we should still be in the same folder that we installed everything. If you're not, make sure you go back there) and type:

<code>grunt</code>

This will run grunt and it will use the configuration that was setup in Gruntfile.js. You will see it run "sass:dist" which runs sass on any sass files that exist (we didnt do anything with this yet). Then it will run "develop:server" - which will actually launch a web server on your machine and deploy your app to it. Leave this running and open a browser window and go to localhost:3000. You should see your basic Express app running!

You'll also notice that your console says "Running 'watch' task" waiting....This is actually really cool. It watches all of your files for changes. As soon as you save any of your files, it will automatcially redeploy the app and it will also automatically refresh your page in the browser. Makes devloping really nice. 
