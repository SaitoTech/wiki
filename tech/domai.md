---
title: Module Conventions
description: 
published: true
date: 2022-08-01T06:56:02.897Z
tags: 
editor: markdown
dateCreated: 2022-08-01T06:56:02.897Z
---

# Module Conventions:

### Third Party Libraries:

Third party libraries should not be used without review and team agreement.

When third party libraries are added these should be hosted by the node and included in …web/saito/ 


### CSS Files:

Saito Components should have their CSS included in the

```` /web/saito/css-imports/````  directory and included dynamically into Saito via the ````/web/saito/saito.css stylesheet````. Modules should put their CSS files in their own /web/css/ directory. Modules may have multiple CSS files.

If you are unsure where CSS should go, please put it into a separate file in the modules css directory and we can port it to the proper place once the application is designed and class names are finalized.


### Templates:

Template files are components that generate HTML. We use them for common UI elements like user-boxes. Template files can be found in the /lib/saito/new-ui/templates directory. All template files should produce well-styled output if used in applications that link to the /web/saito/saito.css stylesheet.

``` 
/lib/saito/new-ui/templates/saito-user.template.js
/lib/saito/new-ui/templates/saito-user-with-controls.template.js
/lib/saito/new-ui/templates/saito-user-with-timestamp.template.js
```


To use a template file, require it at the top of the file that will need to produce the HTML.

```
const SaitoUserTemplate = require(‘./lib/saito/new-ui/templates/saito-user.template.js’);
```

Templates return HTML that displays the component properly if the /web/saito/saito.css file is included in the page. We encourage modules that wish to tweak this core CSS to overwrite the necessary class definitions in their ```/module/web/style.css file.```

````
app.browser.addElementToDom( SaitoUserTemplate(app, mod, publickey) );
````

Developers should note that while template files follow our standard of requiring app and mod as their first two arguments, they typically have arbitrary additional requirements based on the object itself. The template above takes the public key of the user whose box is being displayed, for instance.


### Saito UI Components:

Saito UI Components are UI Components. The difference is that while template files return HTML directly, UI components are objects which are created and then told to render themselves into the DOM.

const SaitoSidebar = require(‘./lib/saito/new-ui/saito-sidebar/saito-sidebar’);

Most UI Components take a query-selector as the third argument to their render function which renders the component into the container specified:

````
let sidebar = new SaitoSidebar(app, mod);
sidebar.render(app, mod, “.saito-container”);
````

Our default set of our Saito UI Components can be found in our ```/lib/saito/new-ui``` directory. There is a direct connection between the names of elements and the CSS class names of their components:


````
/lib/saito/new-ui/saito-header/saito-header.js
/lib/saito/new-ui/saito-overlay/saito-overlay.js
/lib/saito/new-ui/saito-sidebar/saito-sidebar.js
/lib/saito/new-ui/saito-calendar/saito-calendar.js
````

If you are creating your own UI Components we encourage you to look at these main components and follow their style.


### Module UI Components:

Module UI Components work like Saito UI Components., except they are stored in the individual module /lib directory. These UI Components may or may not take a query-selector as the third argument to their render() function: module developers are welcome to hardcode them as required for convenience in app development.

````
/mod/redsquare/lib/menu.js
/mod/redsquare/lib/menu.template.js
````


#### Applications as UI Components:

Some applications allow other modules to add functionality to their interfaces. Most applications permit the chat module to stick a chat-manager box into their left-hand sidebar, and allow the chat module to manage in-application peer-to-peer chat. The settings module also allows other modules to add elements to its control panel.

**The Saito team follows these standards:**

If a component is designed to display full-screen, it will start from a UI Component defined in main.js that uses main.template.js. The starting point for hacking the UI of any existing Saito applications is thus:

	- /mods/module/lib/main.js
	- /mods/module/lib/main.template.js


If a module uses ```respondTo()``` to insert itself into other applications, the component which is inserted should be named main.js as well, but stored in a sub-directory named after the argument. If a module displays a panel in the default “appspace” it should  a module responds to “chat-manager” f that triggers the display of the UI Component. 


These two rules create a simple rule-of-thumb – all components that are called for display by something external to the module itself should start from a main.js file. The /lib directory can thus be organized however the developer wishes, as long as the developer ensures that the parent-level components that are called for display are technically saved as main.js and main.template.js files.


### Example:


Arcade has its own full-screen interface, which is managed by the UI Component ```/lib/main.js``` using the template file ```/lib/main.template.js```.The module javascript file /arcade.js includes this UI Component and calls on it to ```render()``` when the module is called to render itself.

Arcade can respond to requests to insert itself into an “appspace” panel. It stores the UI Component that will render into this panel in its ```/lib/appspace/main.js``` file using the ```/lib/appspace/main.template.js``` file. This component uses a combination of sub-components stored elsewhere in the ```/lib``` directory, including in the appspace sub-directory, but the main.js file is instantly identifiable as the parent component presented for external display.


````
redsquare/lib/main.js			   <---- renders into saito.io/redsquare


/redsquare/lib/main.template.js		   <---- template file for main page


/redsquare/lib/appspace/main.js	       <---- renders into ".appspace" 
                                        <---- respondTo(“appspace”)
                                        <---- expects DIV w/class “appspace"
                                        <---- class “redsquare-appspace"

             
             
             
/redsquare/lib/appspace/sidebar/main.js    <---- renders into ".appspace-sidebar"
                                           <---- respondTo(“appspace-sidebar”)
                                           <---- expects DIV w/class “appspace-sidebar"
                                           <---- class “redsquare-appspace-sidebar"

             
/redsquare/lib/menu.js			        <---- component, does not render into anything
					                          <---- class “redsquare-menu”
````


Following these standards will make application development easier. The location of the file and its position in the directory structure is thus consistent with the classname of the DIV that is designed to contain it, as well as its own internal CSS class definition.




**Rendering Modules as Components**

Modules can be written to render themselves just like UI Components. You can do this by defining the render(app, mod, selector) function in the module itself, so that the third argument is a selector that controls what part of the application is rendered to the screen (and where it is rendered).

UI Components can be given the functionality of modules if they are extended from the UIModTemplate class in the /lib/templates directory. For an example of a UI Component that takes this approach, look at ```/lib/saito/new-ui/saito-sidebar/saito-sidebar.js```. This is useful if you wish to write a UI Component to which other components can be added / removed through **addComponent()** / **removeComponent()** and have the children automatically render themselves when render is called on the parent component.


