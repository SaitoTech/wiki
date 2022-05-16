---
title: Tutorial 1 Deploy and Install Application
description: Deploying and Installing Application in Saito
published: true
date: 2022-05-16T03:01:52.408Z
tags: 
editor: markdown
dateCreated: 2022-03-22T07:07:49.922Z
---

# Tutorial 1 – Deploy and Install a Saito Application

Start by downloading this [ZIP file](/tutorial01_(2).zip). 

***Note**: need to change since org will be deprecated, which contains a very simple application*. You can find an annotated copy of the source code online, and may want to take a quick look. For now let’s move on to uploading and installing it.

![appstore_screenshot.png](/appstore_screenshot.png)

Visit your [Saito Settings](https://saito.io/dev/#email-nav-AppStore) and click on “AppStore” in the application sidebar. We want to upload our new application, so drag that zipfile onto the drag-and-drop upload panel. This transfers the file into your browser and wraps it in a Saito transaction. A submit button will appear when this process is done. Click it.

Congratulations! You’ve just published your application. Technically, you’ve just sent that transaction (containing your app) out into the network along with metadata requesting that the AppStores on the network index and host your application. 

Surprise! If your browser sent the transaction properly, you’ll have received an email confirming your submission. Open this email and you’ll find your unique APP-ID along with a link you can click on to install the application. Anyone can use that link or your APP-ID to find your application. If you ever need to search manually, go back to the AppStore, click to launch the Saito Appstore and search for your APP-ID manually (note: if your application is not found right away, wait a minute until it is finished indexing). You should see this:

Click to view your app details and then click INSTALL. Upgrading your browser takes about 45 seconds. Watch the countdown and wait for your installation to complete. You’ll be asked to confirm you want to upgrade your client before the process is over. Click “CONFIRM”.

![tutorial1appstore.png](/installconfirm.png)

Look at the sidebar and you’ll see the application you just installed. Click on it and click on the button. Looks like this application creates a simple HTML interface and sends a transaction (with data) onto the network s, and then take a look at the [annotated source code](https://github.com/SaitoTech/saito-lite/blob/master/mods/tutorial01/tutorial01.js) to see how easy it was to build.

In our [next tutorial](/tech/tutorial-2-chat) we’ll create an application that can receive transactions in addition to sending them. Before we get to that, there’s something important you may have realized: the Saito AppStore is an application like any other application. Although our tutorial series starts with small applications, there’s no limit to the complexity of the applications that you want to build.

