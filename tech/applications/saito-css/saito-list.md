---
title: Saito-list
description: 
published: true
date: 2022-06-29T14:31:37.640Z
tags: 
editor: markdown
dateCreated: 2022-06-29T08:29:10.675Z
---

# Saito-List

The ```saito-list``` class acts as a container for list components/types that share a similar structure but with important differences

There are 3 major list types:
- saito-list-user
- saito-list-game
- saito-list-chatbox



Each List type can be placed inside the saito-list container:

```1: saito-list-user```
```
    <div class="saito-list">
        <div class="saito-list-user">
            <div class="saito-list-user-image-box">
                <img class="saito-idenitcon" />
            </div>
            <div class="saito-list-user-content-box">
                <div class="saito-username"></div>
                <p></p>
            </div>
        </div>
    </div>
````

Developers may also choose to omit the interior class declarations if they desire.
````
    <div class="saito-list">
        <div class="saito-list-user">
            <div>
                <img/>
            </div>
            <div>
                <div></div>
                <p></p>
            </div> 
        </div>
    </div>
````



```2: saito-list-game```
```
     <div class="saito-list">
        <div class="saito-list-game">
            <div class="saito-list-app-image-box">
                <img class="saito-app-image" />
            </div>
            <div class="saito-list-app-content-box">
                <div class="saito-app-name"></div>
                <p></p>
            </div>
            <div class="saito-list-game-controls">
            </div>
        </div>
    </div>
````
Developers may also choose to omit the interior class declarations if they desire.

```
    <div class="saito-list">
        <div class="saito-list-module">
            <div>
                <img />
            </div>
            <div>
                <div></div>
                <p></p>
            </div>
            <div>
            </div>
        </div>
    </div>
````





```3: saito-list-chat```
````
       <div class="saito-list">
        <div class="saito-list-chatbox">
            <div class="saito-list-user-image-box">
                <img class="saito-identicon" />
            </div>
            <div class="saito-list-user-content-box">
                <div class="saito-username"></div>
                <p></p>
            </div>
            <div class="saito-list-user-timestamp">
            </div>
        </div>
    </div>
````

As usual, developers may also choose to omit the interior class declarations if they desire.
````
    <div class="saito-list">
        <div class="saito-list-chat">
            <div>
                <img />
            </div>
            <div>
                <div></div>
                <p></p>
            </div>
            <div>
            </div>
        </div>
    </div>
````




Developers might need a smaller or larger variant of a list type, with smaller or larger identicon or font-size as the case may be. This can be easily managed by adding specific classes to the list type:
 
- small  : for a smaller list variant
- large  : for a larger list variant



``````
    <div class="saito-list">
        <div class="saito-list-chat small">
            <div>
                <img />
            </div>
            <div>
                <div></div>
                <div></div>
            </div>
            <div>
            </div>
        </div>
    </div>
    
    
        <div class="saito-list">
        <div class="saito-list-chat large">
            <div>
                <img />
            </div>
            <div>
                <div></div>
                <div></div>
            </div>
            <div>
            </div>
        </div>
    </div>
    
    
    
    
    
``````
