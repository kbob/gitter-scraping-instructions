# Scraping Gitter

[Gitter.im](https://gitter.im/) is a chat service for developers.  Sort
of an open source Slack.

It is really unpleasant to review a conversation's history in Gitter.
There is a search function, but it's unwieldy.  And automatic pagination
prevents you from searching in page for more than a handful of messages.

So here are my notes about turning a Gitter room's history into a
static HTML page that you can scroll through and search within.

# Overview

* Install node.js, npm, and gitter-export-room.
* Install this repository.
* Use gitter-export-room.
* Reformat into HTML.
* Open in browser.

# Instructions

## Prerequisites

Install node.js and npm, npm version >= 6.0.  Macports, Homebrew,
apt-get, [node.js installer](https://nodejs.org/en/download/), whatever.

Check out gitter-export-room and install it.

    $ git clone -b patch-1 https://github.com/100ideas/gitter-export-room.git
    $ cd gitter-export-room
    $ sudo npm install -g .

## Get a Token

 * Sign in to https://developer.gitter.im .  You should be shown a token.
 * Select the token, then leave the web page open for future copy/paste.

## Download files

    $ gitter-export-room --token XXXX list
    63ef16bf6c15ebbc318db9b6   SomeProject
    9aa741f60960dd226cd965f1   SomeProject/a_room
    a1d842691b0ccb868581b0ac   SomeOtherProject
    [...]

Find the room you want and use its ID.

    $ gitter-export-room --token XXXX id YYYY | tee some-file.json

With any luck, you'll get a very large JSON file in a few minutes.

## Reformat into HTML

    $ ./fmt-gitter some-file.json > some-file.html

## View in Browser

    $ open some-file.html

That will give you the room's entire history as a single, large HTML page.
