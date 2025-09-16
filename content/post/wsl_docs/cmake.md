---
title: Make and CMake Install
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
show_date: false
# Optional header image (relative to `assets/media/` folder).
header:
  caption: ""
  image: ""
---

## Install Make

Install build essentials and Make first:

```console
sudo apt-get install make
sudo apt-get update && sudo apt-get install build-essential
```

## Install CMake
Download the latest version of the [CMake executable](https://cmake.org/download/#latest). 

In your linux shell run (replacing VERSION with the version you downloaded):

```console
VERSION=4.1.1
cd ~/Downloads
chmod +x cmake-$VERSION-linux-x86_64.sh
sudo ./cmake-$VERSION-linux-x86_64.sh
sudo mv cmake-$VERSION-linux-x86_64 ~/bin/cmake
```

Then add the following line to your `.basrc` or `.zshrc`, replacing the path with the path to cmake install on your system:

```
export PATH=$PATH:$HOME/bin/cmake/bin
```
