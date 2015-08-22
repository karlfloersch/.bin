# .bin - .BashInNuggets!
.BashInNuggets (.bin) is a little collection of my bash scripts that I write when I decide to waste
my time with automating random stuff. Relevant:

![xkcd](https://imgs.xkcd.com/comics/automation.png)

# Table of Contents

  1. [General Installation](#general-installation)
  1. [rundock](#rundock)


# General Installation
Each one of these scripts can be installed seperately or you can grab the whole collection.
There is no real installation process, as these are all just little scripts you can run with:

    $ ./script_name

That's it!  If you want to make these scripts available globally, you can move them into a folder
which is contained in your $PATH variable.  For instance `/usr/local/bin`


*************************************
# rundock
My personal bash script for running disposable development docker containers

## What does it do?
rundock is a simple script using Docker which will create/run a new docker image that mounts your 
current directory as the workspace. I think it's easier to describe with an example...

## Example:
I have a Node.js application already half written. I `cd` into the base directory of my app. It looks
something like this:

    bin/  index.js  lib/  node_modules/  package.json  public/
  
I want to run this application but I don't want to install Node.js on my base machine. I've broken too
many of my Linux boxes by installing loads of development crap.  (Assuming I have Docker installed)
I can now use rundock! I simply call:

    rundock node -w # tells rundock you want to use node as a workspace

And rundock creates a new Docker container using the official Node.js repository 

NOTE: For workspaces, rundock exposes *port 80* on the container side for
accessing your app

[https://hub.docker.com/_/node/](https://hub.docker.com/_/node/), mounts my current directory to that container's workspace, and starts
that container's bash.

Now I can run `node index.js` and I didn't install anything on my base OS (besides Docker of course)!

## How does it handle ports?
On workspaces, port 80 is exposed on the container with -p 80

## How does it handle connecting databases? (linking)
Assuming you already ran `rundock mongo` and `rundock elasticsearch` You can link your docker 
images together using 

    rundock node -w -l mongo -l elasticsearch
    
## Tested to be working Images
- [Node.js](https://hub.docker.com/_/node/)
- [MongoDB](https://hub.docker.com/_/mongo/)
- [ElasticSearch](https://hub.docker.com/_/elasticsearch/)
- [Nginx](https://hub.docker.com/_/nginx/)

