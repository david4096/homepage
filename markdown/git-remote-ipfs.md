# Use ipfs as a git remote

This is still a bit of a shaky process, but it works for me for now, so I thought
I'd share!

## Set up your source repo

You can add a git repo like any other to ipfs, its just a lot of files, so to start
we'll do just that.

This Web page is tracked in git, so we'll use it as a case study. There is plenty of
room for improvement in this process and not a lot of documentation!

```
cd homepage
cp -R .git homepage.git
ipfs add homepage.git -wr
```

This will return a list of ipfs hashes we can use to get at our git tree!

Now the git tree for our project is available on ipfs! We should already be able to
do some interesting things with this. For example, using the ipfs.io http-bridge we
can probably clone it!

```
