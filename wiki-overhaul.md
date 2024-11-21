---
title: dcm install test
description: 
published: true
date: 2024-11-21T20:33:58.978Z
tags: 
editor: markdown
dateCreated: 2024-11-13T20:09:07.715Z
---

# Wiki Overhaul

## Applications

 - either we include the DCM modules in the WIKI (folders follow convention)
 - or applications can link to Github, and modules get /bin directory for DCM txs

## <div id="mods">"Mod" vs "App" Language</div>
![apps-vs-mods.png](/apps-vs-mods.png)

 - always use "application"
 - i.e. applications are listed in the "modules" directory /mods
 - i.e. applications are listed in the "modules" directory /mods



## SLR Developer Structure

 - /tech/applications ✔️✔️
 - /tech/applications/deploy ✔️✔️
 - /tech/tutorials/ ✔️✔️
 - /tech/tutorials/01 etc. ✔️✔️
 - /tech/tutorials/02 etc. ✔️✔️
 - /tech/install ✔️✔️
 - /tech/install/rust ✔️✔️
 - /tech/install/javascript ✔️✔️
 - /tech/compile <--- "what do you want to compile?" ✔️
 - /tech/compile/saito-rust ✔️
 - /tech/compile/saito-lite-rust ✔️✔️
 - /tech/compile/saito-wasm 
 - /tech/compile/saito-js
 - /tech/compile/applications ✔️✔️
 - /tech/config <--- "what do you want to configure" ✔️✔️
 - /tech/config/server <--- configure config/options.conf ✔️
 - /tech/config/network <--- configure config/options.conf 
 - /tech/config/applications <---- configure config/modules.config.js ✔️✔️
 - /tech/config/settings <---- configure UI / wallet / apps ✔️
 

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