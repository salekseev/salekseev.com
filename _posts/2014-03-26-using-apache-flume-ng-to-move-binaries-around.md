---
layout: post
title: "Using Apache Flume-NG to move binaries around"
date: 2014-03-26 16:32:19 -0400
comments: true
categories: [linux, hadoop, flume-ng]
---

Need to move small binary files from one server to the other? Flume-NG to the
rescue! It supports complex topologies and is quite fast about it.

1. Install flume-ng on your server (Cloudera's CDH4 packages are nice).

2. Set up a source and a destination directories and a configuration
   file, in our case flume-ng-agent.conf.

{% gist salekseev/310c94d7f12d40cd97d9 %}

3. Launch a flume agent

<code>
flume-ng agent --conf-file flume-ng-agent.conf --name a1 -Dflume.root.logger=INFO,console
</code>

4. Drop some binaries into the ~/source folder and watch them appear in
   the ~/dest folder. Originals are by default renamed with a .COMPLETE
suffix but could also be removed.

The only downside is the the default serializer for file_roll sink does
not preserve the original filename.

Always a good idea to look at the docs for more info -
[http://archive-primary.cloudera.com/cdh4/cdh/4/flume-ng/](http://archive-primary.cloudera.com/cdh4/cdh/4/flume-ng/).
