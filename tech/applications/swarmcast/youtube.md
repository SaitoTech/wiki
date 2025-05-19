---
title: Swarmcasting on Youtube
description: How to Setup Saito Swarmcasting on Youtube
published: true
date: 2025-05-19T15:27:19.150Z
tags: 
editor: markdown
dateCreated: 2024-08-27T05:33:30.520Z
---

# Swarmcasting on Youtube

You can connect a [Swarmcast](https://saito.io/swarmcast) with YouTube by providing a YouTube Stream Key when asked. Youtube is not very clear about how to setup your account to get this key, and it is easy to run into problems if you're streaming off a slower internet connection, so we are providing straightforward directions below.

## 1. Visit Youtube

Click on the top-right menu and select "Youtube Studio".

<br />
<img src="/media_gallery/youtube_studio.png" style="width:300px;" />


## 2. Navigate to "Live Streaming" Feature

Click on the "Create" button and then the "Go Live" menu option.

<br />
<img src="/media_gallery/youtube_create.png" style="width:300px;" />

NOTE: if this is your first time setting up a swarmcast, Youtube will ask you to enable live streaming for your account -- it usually takes about 24 hours for Youtube to do this, so you should do this at least a day in advance of your first swarmcast. Follow the remainder of the instructions on this page once this step is completed.


## 3. Create a Stream (and get your Stream Key)

If it is your first time setting up a Youtube Stream, you'll see a popup asking you whether you want to start streaming now (using your webcam) or whether you want to schedule a stream for later. You always want to "schedule" your stream as this tells Youtube you are using something other than your webcam to capture the video and audio.

<br />
<img src="/youtube_stream2.png" style="width:400px" />

You'll now get a screen which invites you to provide a title and description. You can scroll down for many more options, including the category for the stream and whether the broadcast is suitable for children (tip: advertising is minimized on kid-friendly shows). Any settings you want are fine. Click NEXT when done.

<br />
<img src="/youtube_stream1.png" style="width:600px" />

There are two more pages of options you'll need to click past before you will be given a stream key. You don't need to worry too much about the settings. Once you have clicked through the final page you'll be returned to the dashboard with a page that looks something like the following:

<br />
<img src="/media_gallery/youtube_live.png" style="width:600px" />

Your <b>STREAM KEY</b> is below the preview video in the "Stream settings" section of the Youtube dashboard. You can click on the copy button to copy it into your clipboard. If you have issues or are on a slower Internet connection see the troubleshooting section for help reducing bandwidth needed to stream. Otherwise, just copy this <b>STREAM KEY</b> and provide it to your Saito application when you click the Youtube button and are prompted for it as below:

<br />
<img src="/step4-enterkey.png" style="width:500px" />


## 5. Troubleshooting

Youtube defaults to expecting a fast connection that can consume up to 30 MBPS in data-throughput. This provides a high-quality video, but can be overwhelming for browsers outside the United States or on slower network connections. It can also be a problem if you are streaming to multiple peers. So if you have a slower connection or run into problems, we recommend updating your Youtube settings to hardcode a slower connection.

To do this you will need to create ANOTHER stream key that is hardcoded to a lower bitrate. Start by clicking on that select box on the front page and choose "Create new stream key" as below:

</br>
<img src="/media_gallery/youtube/youtube_create_new_stream_key.png" style="width:400px" />

A new overlay will pop up -- you can provide name for your new stream key so that you can re-use these settings in the future. The important thing is to select the options "Turn on manual setttings" and then choose a lower resolution option. We recommend the 480p option if you're on a slower internet connection. It still works great!

</br>
<img src="/media_gallery/youtube/youtube_stream_manual_settings.png" style="width:400px" />




