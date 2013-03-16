khs-logger.js
=============

Java Script logging library with support for remote logging. 

Visual Backbone.js view/template inspector, outlines and inspects backbone.js views for developer support. 

Getting Started
---------------

Download latest release here [https://github.com/in-the-keyhole/khs-logger/archive/0.0.3.zip] unzip in javascript folder

Load using script tags, jQuery is the only required dependency

     <script>lib/khs-logger.js</script>
     
Or as require.js AMD module


	 paths : {
		...
		'jquery' : 'libs/jquery-1.7.2',
		'log' : 'libs/khs.logger'
	 },
	 shim: {
		//khs-logger depends on jQuery
		'log':['jquery']
	 }

#####Note: khs-logger is a true AMD module, and can be loaded this way if desired:
	 require( ["libs/khs-logger"], function(logger) {
		logger.info("loaded with AMD");
	 }

Logging
-------
Formatted log messages to your applications using log levels... 

     // Log expressions 
     $.Log.info("Log an info message");
         
     // debug 
     $.Log.debug("Log a debug message");
          
Set log level (valid levels log,info,debug,warn,error)
 
     $.Log.level = $.LogLevel.debug;    
 
Define remote logging URL
 
     $.Log.remoteUrl = "sherpa/log;  //restful url from origin <origin>/sherpa/log{message}
      
Set remote logging level

     $.Log.remoteLevel = $.LogLevel.error;
     
Before send call back function, so you can manipulate request headers

     $.Log.beforeSend = function(xhr,opts) { // to stuff, ie. add security token is necessary};     
     
Capture all errors and log to remote end point                   
  
     window.onerror = function(message, url, linenumber) {
		$.Log.error(message+"line:"+linenumber+"url:"+url);
	 }


View Inspector
--------------
Inspect div's, really helpful with Backbone.js views and html templates, visually shows view/template boundaries, here's how to apply.

Mousing over div's outlines and displays information by hitting CRTL ENTER, open inspector view with DBL Click, see screen shot below.
View inspector has been enabled at this site [http://cgrok.com] give it a try...

![My image](https://raw.github.com/in-the-keyhole/khs-logger/master/screen.png)


Turn inpsector on

     $.Log.inspect(); // active outliner with CTRL-ENTER, open inspector with DBL CLICK

Mark and display a DIV on mouse over... 

     $.Log.mark(<div>,<message>,<optional JSON object>);
     
Example applied to backbone.js view with $.Log.mark(...) 
     
     ...
     render : function(eventName) {
			var compiled_template = _.template(Template);
			this.$el.html(compiled_template(this.model.toJSON()));
                        $.Log.mark(this.$el,"navBarCatRefView.js -> navbar-cateory-reference.html",this.model.toJSON());	
			return this;
	 }, ..

