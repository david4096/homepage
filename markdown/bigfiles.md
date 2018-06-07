# Big Files on ipfs

This post is meant to be a test of being able to use ipfs to share files
without too much thought.

We'll watch an ogg that hopefully can stream from ipfs!

## The old fashioned way

First, we'll embed the http version hosted by archive.org.

It looks like this:

```
<video src="https://archive.org/download/DWebSummit2016_Keynote_Tim_Berners_Lee/DWebSummit2016_Keynote_Tim_Berners_Lee.ogv" type="video/ogg" controls width="320" height="240"></video>
```

<video src="https://archive.org/download/DWebSummit2016_Keynote_Tim_Berners_Lee/DWebSummit2016_Keynote_Tim_Berners_Lee.ogv" type="video/ogg" controls width="320" height="240">
</video>

Note we're not actually streaming this file, but simply downloading it 
faster than we are viewing it.

## The decent way

Then, we'll download it, move it to the public directory of the blog, 
and use `ipscend` to upload it to ipfs.

```
cd homepage
mkdir public/videos
cd public/videos
wget https://archive.org/download/DWebSummit2016_Keynote_Tim_Berners_Lee/DWebSummit2016_Keynote_Tim_Berners_Lee.ogv
cd ../..
ipscend publish
```

This will take a few minutes depending on your connection.

The tag is pretty much the same, except since this Web page is hosted on ipfs, it is served from a 
relative path.

```
<video src="../videos/DWebSummit2016_Keynote_Tim_Berners_Lee.ogv" controls type="video/ogg" width="320" height="240"></video>
```

<video src="../videos/DWebSummit2016_Keynote_Tim_Berners_Lee.ogv" controls type="video/ogg" width="320" height="240"></video>

It should load alright, but I observed some odd behavior trying to scroll around as it loaded.

### Speed notes

We're using the decentralized web here, so if you have a copy of this file locally, the data doesn't need
to transit through a central service to reach you. There is no time waiting to upload, but if you're ipfs
daemon goes offline before it has been replicated across the network, it might not be complete!

Sometimes it takes a little while to resolve and buffer the video into the frame, but I was able to watch 
smoothly over the decent web.

## Going further

Any Web technology should be usable in some way in the decentralized Web. For example, chat services that create
ad-hoc relationships between browsers like Web RTC might be used to create bridges between the decent- and
centralized Webs.

__________________

[Go home](../)
