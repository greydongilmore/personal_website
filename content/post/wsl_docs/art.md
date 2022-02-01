---
title: Installing Automatic Registration Toolbox
subtitle:
summary:
date: "2018-06-28T00:00:00Z"

reading_time: false  # Show estimated reading time?
share: false  # Show social sharing links?
profile: false  # Show author profile?
comments: false  # Show comments?
private: false
tags: ["Neuro Software"]
authors: ["admin"]

# Optional header image (relative to `assets/media/` folder).
header:
  caption: ""
  image: ""
---

## Download ART

Download the newest version of [ART](https://www.nitrc.org/projects/art/)

Make a new directory for the install and extract the tar package into it:

```console
mkdir ~/Applications/ART
cd ~/Applications/ART
tar -xvzf /mnt/c/Users/*[your_username]*/Downloads/acpcdetect2.0*.tar.gz
```

## Post Configuration

Set the ```ARTHOME``` environment variable and add the binary directory to your PATH by editing your ```~/.bashrc``` file:

```console
vim ~/.basrc
```

Add these lines to the end:

```
export ARTHOME=/path/to/ART
export PATH=$ARTHOME/bin:$PATH
```

## Confirm Installation

Execute `acpcdetect` by running command in terminal

You may get an error when executing ```acpcdetect```:

```console
acpcdetect: error while loading shared libraries: liblapack.so.3: cannot open shared object file: No such file or directory
```

If you get this error, run the following:

```console
sudo apt-get install libatlas-base-dev
```

You will also need to install ```pnmtopng```

```console
sudo apt-get install -y pnmtopng
```
