# homepage powered by ipfs

I don't have to tell you things are bad, everybody knows things are bad.
A gigabit connection gets a trickle of content, ad delivery and "user 
analytics" spend more energy than we do reading and writing blog posts. 
Web developers keep a bottle of tequila under the desk, botnets and 
spiders are running rampant on networks. And no one seems to seem to 
be able to do a thing about it or cares!

I want you to get up, go to your windows, open them and say, "I'm mad 
as hell, and I'm not gonna take it anymore!"

## The Inter-Planetary File System

Of course I'm not here to tell you that there is a magical solution 
to being a modern citizen of the Web. At every turn one is faced with 
decisions that are particular to acting in that medium, a medium 
which has no guarantees over the permanence of one's content.

[IPFS](https://ipfs.io/) is meant to allow a peer-to-peer file with 
some guarantees over whether a Web site will be there when you come 
back tomorrow. If you've ever tried going back to bookmarks one, 
two, or five years old, you understand the clear demonstrated need 
for a new approach to the Web.

I first downloaded `golang` from available apt repositories, and then
downloaded and installed the `go-ipfs` client and daemon.

```
sudo apt-get install golang -y
wget https://dist.ipfs.io/go-ipfs/v0.4.15/go-ipfs_v0.4.15_linux-amd64.tar.gz
tar -zxvf go-ipfs_v0.4.15_linux-amd64.tar.gz
cd go-ipfs
sudo sh ./install.sh
```

This will get ipfs up and running, follow the on screen instructions to 
check out the ipfs readme:

```
ipfs cat /ipfs/QmS4ustL54uo8FzR9455qaxZwuMiUhyvMcX9Ba8nUH4uVv/readme
```

You can now start the daemon with `ipfs daemon`, we'll use it in a moment.

## ipscend makes it easy

ipfs lets us manage file's as hashes. It has a lot of features that we 
will completely gloss over because we're just trying to set up a homepage, 
not get funding for a startup.

[ipscend](https://ipfs.io/blog/3-ipscend/) gives us a nice interface for managing files that could represent 
static content to serve a Web site! You'll need nodejs for this part.

```
sudo apt-get install npm -y
sudo npm install -g ipscend
```

We now have the ipscend client that can be used to work with documents 
to create a publishing workflow!

## Just Give Me My Web Page

Websites don't have to be much to start, so don't worry about what you have 
to say, just know you can say it in an interplanetary way.

We'll make a new directory and set up an ipscend project first.

```
mkdir homepage
cd homepage
ipscend init
mkdir public
```

Alright, now we'll start with a very simple homepage and preview the 
output, we haven't yet put anything on the ipfs so don't worry about
typos!

```
echo "Under construction!" > public/index.html
ipscend preview
```

This starts a local Web server and hosts a preview of what your content 
will look like when served by ipfs. One difference is that since the 
files are local, they'll load instantly.

If you're ready to upload your homepage, do `ipscend publish`!

This will return you a URL you can put into a Web browser to view your 
content, now served over the ipfs!

This one originally got: 

> [http://localhost:8080/ipfs/QmXRnxqkz3m9YkcMxSaAG29CVoqgkVYMwCLDvrrC3zsiM4](http://ipfs.io/ipfs/QmXRnxqkz3m9YkcMxSaAG29CVoqgkVYMwCLDvrrC3zsiM4)
> [http://ipfs.io/ipfs/QmXRnxqkz3m9YkcMxSaAG29CVoqgkVYMwCLDvrrC3zsiM4](http://ipfs.io/ipfs/QmXRnxqkz3m9YkcMxSaAG29CVoqgkVYMwCLDvrrC3zsiM4)

So, you're done, if you just wanted to get started with ipscend, you're 
done. For the rest on what went in to this post, read on!

### Caveats

Other nodes might not pick up your data right away, so the file will 
probably be served from your local computer. After accessing my homepage
a couple of times, I closed the ipfs daemon to give myself some 
confidence that it wouldn't just disappear.

The other big caveat is `ipfs.i/ipfs/<hash>` relies someone maintaining 
DNS records. You can send your friends the second URL, but if ipfs.io forgets to pay their 
domain name registration fees, it will break. This doesn't mean the Web 
page itself goes away, but if its the only link people have it might as 
well have.

[ipscend has great [documentation on setting up your own DNS entry](https://github.com/diasdavid/ipscend#use-ipfs-to-host-your-webpage-using-a-standard-domain-includes-cool-dns-trick).
This will let you point to your homepage using your own domain name!

## Using git with it

ipscend has great docs on setting up and viewing versions of your 
published data. I decided to track changes using git as well. This is nice 
because I can make commit comments about changes, and work more 
adeptly with the history.

```
git init .
git add .
git commit -m "Initial commit"
```

This is nice, but simply stores the history on the local machine. We aim to
not rely on centralized services, and a silicon and plastic box is certainly 
a centralization of the history of our homepage we would soon lose.

### git-remote-ipfs

Although we could use ipscend itself to host the git repository data, git itself 
has a more elegant concept of `remotes`. Remotes allow one to define locations where 
source trees are available, including http and ssh.

Using ipfs as a git remote is certainly possible and would let us nicely 
separate the authoring workflow from publishing.

## Static site generators

By laying out your content in a specific way, static site generators enable you to 
create rich Web sites without pasting together a lot of HTML. For now, we'll simply
hand generate a home page and the link to this post, however, using a static 
site generator could add things like search, timestamps, headers/footers and author 
info.

```
mkdir markdown
nano markdown/ipscend.json
# Write the markdown blog post!
sudo apt install pandoc
pandoc -t html markdown/ipscend.md > public/ipscend.html
# Add a link to the post!
echo "<p><a href="ipscend.html">homepage powered by ipfs</a>" >> public/index.html
```

Just because ipfs is the permanent Web doesn't mean your site can't be under construction!

Be sure to check out [ipfs-blog](https://github.com/noffle/ipfs-blog), which very much inspired this post!

## Remember your keys

When I set up the ipfs daemon, it generated a keypair which I use to guarantee 
that only I can modify data I have created on ipfs. If you want to be able 
to maintain write access to your ipfs hashes, you'll need to keep those keys 
around.


### Future ipfs posts

Getting on the decentralized web is getting easier and easier, and I'm ashamed 
it took Cambridge Analytica, Github acquired by Microsoft, and GDPR to finally 
convince me that it is worth going to the extra effort.

The decentralized Web is not just made up of ipfs, but a host of other technologies 
and good people behind them. I hope you'll take the time to check out some other 
projects like [Secure Scuttlebutt](http://scuttlebutt.nz)'s [Patchwork](https://github.com/ssbc/patchwork) and 
[Mastodon](https://joinmastodon.org/) that do a much better job of lowering the 
barrier to entry to the decentralized Web.

________________________

<a href="index.html">Go home</a>
