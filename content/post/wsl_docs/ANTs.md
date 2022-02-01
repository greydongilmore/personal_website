---
title: Install Advanced Normalization Tools
subtitle:
summary:
date: "2020-09-28T00:00:00Z"

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

## Get the latest ANTs code

Download the latest code into an arbitrary directory, I use ~/code:

```console
mkdir ~/code 
cd ~/code
git clone https://github.com/ANTsX/ANTs.git
```
You will also need to install the ZLIB libraries:

```console
sudo apt-get install zlib1g-dev
```

## Run CMake/Make

I install my applications in ```~/Applications```, however the following will install ANTs in ```~/bin```:

```console
mkdir -p ~/bin/ants
cd ~/bin/ants
ccmake ~/code/ANTs
```

Hit __'c'__ to do an initial configuration. CMake will do some checking and then present options for review. Hit __'c'__ again to do another round of configuration. If there are no errors, you're ready to generate the make files by pressing __'g'__.

Now you are back at the command line, it's time to compile:

```console
make
```

This compiles in the most resource-efficient manner. To save time, you can use multiple threads, for example:

```console
make -j 2
```

## Post-install Configuration

If you want to use ANTs scripts, copy them from the source directory ```Scripts/``` to the bin directory where ```antsRegistration``` etc are located:

```console
cp -r ~/bin/ants/Scripts/* ~/bin/ants/bin/
```

Assuming you've built in ```~/bin/ants```, there will now be a binary directory ```~/bin/ants/bin```, containing the programs (and scripts if you've included them). The scripts additionally require ANTSPATH to point to the bin directory including a trailing slash.

You will need to edit your ```.bashrc``` or ```.profile``` file by adding the following lines:

```console
export ANTSPATH=${HOME}/bin/ants/bin
export PATH=${ANTSPATH}:$PATH
```

Now check this worked correctly:

```console
which antsRegistration
```
