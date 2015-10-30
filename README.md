# M13—The Pragmatic Way to Create Content

The M13 system is a simple way to create great-looking interactive
content for technical material. It makes it easy to create text, code
listings, interactive terminal sessions, multi-level content, and
quizzes.

## Getting Started


1. Install the m13 tools on your machine if you haven't already:

        $ curl -fLsS https://raw.githubusercontent.com/pragdave/m13/master/install/osx.sh | sh


2. In the directory containing this README, use the command

        $ m13

   This should build an HTML file containing the m13 sample document.

## What's Going On

The m13 system has the concept of _necklaces_ and _pearls_.

A pearl is a (relatively) self-contained chunk of documentation. It is packaged in such a way that you can use it, and other people can use it (and you get a royalty payment when they do).

A necklace is a complete document, assembled from a number of pearls (both your own and potentially other people's). You can also add your own commentary between pearls (if you like). This means that your necklace can build a narrative by pulling in pearls from multiple sources.

## What To Do Now

1. Have a look at `sample.md`. It contains examples of most of the markup we support.

2. Look at the file `Necklace`. It acts as a kind of manifest, telling our tools how to build your document.

3. Then look in the `pearls` directory. Here's where you store the pearls you create, each in its own subdirectory.

    The trick here is to try to make each pearl free-standing. This will encourage others to use them.

5. Start writing. Update the Necklace file to point to your first content document, and use `m13` to build it as you go.
