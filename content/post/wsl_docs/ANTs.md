---
title: ANTs (Advanced Normalization Tools) Install
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
show_date: false

# Optional header image (relative to `assets/media/` folder).
header:
  caption: ""
  image: ""
---

## Get the latest ANTs code

You will need to install the ZLIB libraries:

```console
sudo apt install zlib1g-dev
```

Obtain the newest version of [ANTs](https://github.com/ANTsX/ANTs/releases/latest) by running the following:

```console
mkdir -p ~/Documents/code/ants_source
cd ~/Documents/code/ants_source
git clone https://github.com/ANTsX/ANTs.git .
```

## Run CMake/Make

Make the build directory.

The default install location is `/opt/ANTs`, which falls on your PATH. This is the easiest location to install. If you want to install somewhere else then specify the path in the `CMAKE_INSTALL_PREFIX` variable.

```console
mkdir -p ~/bin/ants
cd ~/bin/ants
ccmake ~/Documents/code/ants_source
```

Hit __'c'__ to do an initial configuration. CMAKE will do some checking and then present options for review. Hit __'c'__ again to do another round of configuration. If there are no errors, you're ready to generate the make files by pressing __'g'__.

Now you are back at the command line, it's time to compile:

```console
make -j
```

```console
cd ~/bin/ants/ANTS-build
sudo make install
```

## Post-install Configuration

You will need to edit your `.bashrc` or `.zshrc` file by adding the following lines:

```console
export PATH=$PATH:/opt/ANTs/bin
```

Now check this worked correctly:

```console
which antsRegistration
```
