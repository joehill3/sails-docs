This table routes urls to controllers/actions.

# Resourceful Routing
If the URL is not specified in **config/routes.js**, the default route for a URL is:
**/:controller/:action/:id**
where **:controller**, **:action**, and the **:id** request parameter are derived from the url

If **:action** is not specified, Sails will redirect to the appropriate action.  Out of the box,
Sails supports RESTful resourceful route conventions, as used in Backbone.js.

```
	# Backbone Conventions
	GET   :	/:controller			=> findAll()
	GET   :	/:controller/read/:id		=> find(id)
	POST  :	/:controller/create		=> create()
	POST  :	/:controller/create/:id		=> create(id)
	PUT   :	/:controller/update/:id		=> update(id)
	DELETE:	/:controller/destroy/:id	=> destroy(id)

	# You can also explicitly state the action
	GET   :	/:controller/findAll		=> findAll()
	GET   :	/:controller/find/:id		=> find(id)
	POST  :	/:controller/create		=> create(id)
	PUT   :	/:controller/update/:id		=> update(id)
	DELETE:	/:controller/destroy/:id	=> destroy(id)
```

If the requested controller/action doesn't exist:
  - if a view exists ( **/views/:controller/:action.ejs** ), Sails will render that view
  - if no view exists, but a model exists, Sails will automatically generate a JSON API for the 
  	model which matches **:controller**.
  - if no view OR model exists, Sails will respond with a 404.

# Custom Routes
You can define your own custom routes in **config/routes.js**

```javascript
module.exports.routes = {
	// To route the home page to the "index" action of the "home" controller:
	'/': {
		controller: 'home'
	}

	// Additional routes might look like:
	'/whateverYouWant': {
		controller: 'someController',
		action: 'someAction'
	}

	// If you want to set up a route only for a particular HTTP method/verb 
	// (GET, POST, PUT, DELETE) you can specify the verb before the path:
	'post /signup': {
		controller: 'auth',
		action: 'signup'
	}

	// Keep in mind default routes exist for each of your controllers
	// So if you have a UserController with an action called "juggle" 
	// a route will be automatically exist mapping it to /user/juggle.
	//
	// Additionally, unless you override them, new controllers will have 
	// create(), find(), findAll(), update(), and destroy() actions, 
	// and routes will exist for them as follows:

	/*

	// Standard RESTful routing
	// (if index is not defined, findAll will be used)
	'get /user': {
		controller	: 'user',
		action		: 'index'
	}
	'get /user/:id': {
		controller	: 'user',
		action		: 'find'
	}
	'post /user': {
		controller	: 'user',
		action		: 'create'
	}
	'put /user/:id': {
		controller	: 'user',
		action		: 'update'
	}
	'delete /user/:id': {
		controller	: 'user',
		action		: 'destroy'
	}
	*/
};

```

[![githalytics.com alpha](https://cruel-carlota.pagodabox.com/8acf2fc2ca0aca8a3018e355ad776ed7 "githalytics.com")](http://githalytics.com/balderdashy/sails/wiki/routes)