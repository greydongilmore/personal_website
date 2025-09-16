---
title: Freesurfer Installation
subtitle:
summary:
date:

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

## Download software

Download the `.deb` file for [Freesurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/rel7downloads).

Run the following command (replacing the filename with the one you downloaded):

```console
cd ~/Downloads
sudo dpkg -i freesurfer_ubuntu22-8.1.0_amd64.deb
```

You will also need to install some dependancies:

```console
sudo apt-get install tcsh
sudo apt-get install libglu1
sudo apt-get install libxss1
```

## Post-Install Configurations

Add Freesurfer to your path:

```console
echo "FREESURFER_HOME=/usr/local/freesurfer" >> ~/.bashrc
echo 'source $FREESURFER_HOME/SetUpFreeSurfer.sh' >> ~/.bashrc
```

If you have run the install correctly you will see this output when you close and open a new terminal window:

```console
Setting up environment for FreeSurfer/FS-FAST (and FSL)
FREESURFER_HOME /usr/local/freesurfer
FSFAST_HOME     /usr/local/freesurfer/fsfast
FSF_OUTPUT_FORMAT nii
SUBJECTS_DIR    /usr/local/freesurfer/subjects
MNI_DIR         /usr/local/freesurfer/mni
```

## Define subjects_dir

FreeSurfer requires an environment variable called `SUBJECTS_DIR`. This is the directory where subject data is stored, put this in your `~/.bashrc` or `~/.zshrc`:

```console
export SUBJECTS_DIR=<path to subject data>
```

## Obtain license

You will need to obtain a [license key](https://surfer.nmr.mgh.harvard.edu/registration.html).

Once you obtain the `license.txt` key file, copy it to your FreeSurfer installation directory. This is also the location defined by the `FREESURFER_HOME` environment variable.

```console
sudo mv ~/Downloads/license.txt $FREESURFER_HOME
```
