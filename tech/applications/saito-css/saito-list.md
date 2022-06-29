---
title: Saito-list
description: 
published: true
date: 2022-06-29T08:50:36.757Z
tags: 
editor: markdown
dateCreated: 2022-06-29T08:29:10.675Z
---

# Saito-List

The ```saito-list``` class acts as a container for list components that share a similar structure but with important differences

There are 3 major list types:
- saito-list-user
- saito-list-module
- saito-list-chat



Each List type can be placed inside the saito-list container:

```1: saito-list-user```
```
  <div class="saito-list">
        <div class="saito-list-user">
            <div class="saito-idenitcon">
                <img/>
            </div>
            <div class="saito-userinfo">
                <div></div>
                <div></div>
            </div>
            <div class="saito-usercontrol">
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
                <div></div>
            </div>
            <div>
            </div>
        </div>
    </div>
````



```2: saito-list-module```
```
    <div class="saito-list">
        <div class="saito-list-module">
            <div class="saito-modulepicture">
                <img />
            </div>
            <div class="saito-moduleinfo">
                <div></div>
                <div></div>
            </div>
            <div class="saito-modulecontrol">
            </div>
        </div>
    </div>
````
As usual, developers may also choose to omit the interior class declarations if they desire.

```
    <div class="saito-list">
        <div class="saito-list-module">
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
````






````
    <div class="saito-list">
        <div class="saito-list-chat">
            <div class="saito-modulepicture">
                <img />
            </div>
            <div class="saito-chatinfo">
                <div></div>
                <div></div>
            </div>
            <div class="saito-chatcontrol">
            </div>
        </div>
    </div>
````