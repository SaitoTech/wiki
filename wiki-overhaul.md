---
title: dcm install test
description: 
published: true
date: 2024-11-17T05:11:34.352Z
tags: 
editor: markdown
dateCreated: 2024-11-13T20:09:07.715Z
---

# Wiki Overhaul



## <div id="app">Psuedo App Store - Dynamically Compiled Module Install</div>

DCM applications should be installable form the wiki.

1. Is it possible to host the files on the Wiki? [yes](/tutorial01.saito)
2. Can any install steps be automated?

**Problem:** Updating these app files is a pain.

It would be nice if they were just hosted on Github and updated there - Wiki would provide a link to that folder in the repo.

**Idea**:
Move all mods into a seperate Github Repo.

* This is how third-praty mods will be hosted already
* Serves as a page for the app which is better suited than a Wiki page - [example](https://github.com/notable/notable)
* That page is updated with the app
* Wiki can link to those repos

<!--An app can be hosted which fethes and installs from such a link, or installs a user uploaded file for more advanced users wishing to install trustlessly i.e. have access to source code.-->

## <div id="mods">"Mod" vs "App" Language</div>
![apps-vs-mods.png](/apps-vs-mods.png)

Saito Applications are Saito Modules that have a user interface.

## SLR Developer Structure

"App Development" page that has links to everything an SLR dev needs in the order they will need them:

1. Running a Node:
		- [/tech/install](/tech/install)
    		- Saito-Rust				[/tech/install/rust](/tech/install/rust)
        - Saito-Lite-Rust		[/tech/install/javascript](/tech/install/javascript)

 ( assumption : anyone coming here wants to download or install node software )
 ( goal : get to the point Saito available on localhost:12101 )
 

2. Build Applications:
	  [/tech/applications/](/tech/applications/)
    [/tech/tutorials](/tech/tutorials)

		- they need to 
    		- how to run a node but specifically SLR
        - configure the modules installed on the server
        - compile and editing / recompile
		- tutorials 
    - link to APIs
    		- by repo

 ( assumption, anyone coming here wants to build apps )
 ( goal : get to the point Saito available on localhost )


3. Deploy Applications			[/tech/applications/deploy](/tech/applications/deploy)
		- you can deploy your applications in various ways
    		- run a server that hosts them
        - compile them into dynamic modules
        
(this is the only existing **deploy** page currently https://wiki.saito.io/en/tech/javascript/deployment) 
(this has info on **DCM 'deployment'** and more https://wiki.saito.io/en/tech/compile)

4. Documentation
	- core development section here, highly technical, no-one should click unless they are willing to wade through DOCUMENTATION, so the content is less critical
  
  
  
  SUBPAGES;

- Current page housing **config information**: https://wiki.saito.io/en/tech/compile

2. Configure (not main menu, but own part of tree)
	( too ambiguous to have as main menu )
  - how to edit modules.config.js
  - other configuration files and what they do

	- config options for the server
			/tech/config <--- "what do you want to configure"
			/tech/config/server <--- options.conf
      /tech/config/network <--- options.conf
      /tech/config/applications <---- config/modules.config.js
      /tech/config/settings <---- unsure / this would be coding modules Settings
      
	/tech/configure or /tech/applications/config


3. Compiling. (not main menu, but own part of tree)
	/tech/compile <--- "what do you want to compile?"
		- Saito Rust				/tech/compile/saito-rust
    - Saito Wasm			/tech/compile/saito-rust
    - Saito JS			/tech/compile/saito-rust
    - Saito Lite Rust			/tech/compile/saito-rust
    - Applications			/tech/compile/saito-rust
    
  4. Tutorials (main menu), but linked from Build Applications as well
  	/tech/tutorials
  
  (assumption: users or ignorant devs who want a sense of hwo to do things)




OTHER:

/ applications page should link to doc that helps users "install" apps
  







3. AppStore 
4. Docs

Then there can be just two pages under *Development* sidebar category 
1. App Development
2. Core Development