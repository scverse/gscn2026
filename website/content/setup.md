+++
title = "Setup"
subtitle = "One environment, one kernel. About half an hour, most of it unattended."
+++

Everything in this workshop runs on your own laptop. You install one Anaconda
environment and register it as one Jupyter kernel, and that covers both days. Day 1
opens with a setup hour from 12:00 to 13:00 where we go through this together, so if
something below does not work, bring it there.

Each step ends with a check you can run.

<!--more-->

You need about 6 GB of free disk space. The environment takes 2.7 GB once installed and
the data another 1 GB.

## Step 1: install Anaconda

Anaconda gives you Python and the `conda` command. If you already have a working conda,
whether that is Anaconda, Miniconda or Miniforge, go straight to step 2.

Download it from [anaconda.com/download](https://www.anaconda.com/download). The site
asks you to register, and there is a "Skip registration" link under the form if you would
rather not.

### Windows

Take the 64-Bit Graphical Installer and follow the
[Windows guide](https://www.anaconda.com/docs/getting-started/anaconda/install/windows-gui-install).
Three of the installer's choices matter:

1. Pick **Just Me**. Installing for all users needs administrator rights and causes
   permission problems later.
2. Accept the default install location. If you change it, use a path without spaces or
   special characters.
3. Leave "Add Anaconda3 to my PATH environment variable" unticked. It is unticked by
   default, and you will use the Anaconda Prompt instead.

### macOS

Take the Graphical Installer and follow the
[macOS guide](https://www.anaconda.com/docs/getting-started/anaconda/install/mac-gui-install).
Apple silicon and Intel Macs need different installers, and the download page picks the
right one for you. Intel Macs are no longer built for new releases, so on an older Intel
machine take the newest archived version from
[repo.anaconda.com/archive](https://repo.anaconda.com/archive/).

Accept the default install location. The installer sets up your shell.

### Linux

Follow the [Linux guide](https://www.anaconda.com/docs/getting-started/anaconda/install/linux-install).
Download the `.sh` installer, run it, and answer `yes` when it offers to initialise your
shell:

```
bash ~/Downloads/Anaconda3-*-Linux-*.sh
```

### Check

Open a new terminal. On Windows, search the Start menu for **Anaconda Prompt** and open
that one, not the ordinary Command Prompt or PowerShell. On macOS open Terminal, on Linux
whatever you normally use.

The line you type on should start with `(base)`:

```
(base) C:\Users\yourname>
```

Then run:

```
conda --version
```

It prints a version number. If your prompt does not say `(base)`, or the shell does not
recognise `conda`, see [troubleshooting](#troubleshooting) at the bottom.

## Step 2: download the workshop materials

The notebooks and the environment file are in the
[materials repository](https://github.com/scverse/202609_workshop_GSCN).

With git:

```
git clone https://github.com/scverse/202609_workshop_GSCN.git
```

Without git, open the
[repository](https://github.com/scverse/202609_workshop_GSCN) in your browser, click the
green **Code** button, choose **Download ZIP**, and unzip it somewhere you will find
again. Desktop or Documents both work. Use a path without spaces or umlauts if you can,
and on Windows move it out of the Downloads folder, where unzipped copies are easy to
lose track of.

## Step 3: move into that folder

Your terminal has to be inside the folder you just downloaded before anything else works.

Type `cd`, then a space, then the path of the folder. To get the path in:

- **Windows:** find the folder in File Explorer, hold Shift, right-click it, choose
  **Copy as path**, then right-click in the Anaconda Prompt to paste.
- **macOS:** drag the folder from Finder onto the Terminal window.
- **Linux:** most file managers offer "Open in Terminal" on right-click, which skips this
  entirely.

Press Enter, then look at what is around you:

```
dir          (Windows)
ls           (macOS and Linux)
```

You are in the right place if you can see `environment.yml` and a `notebooks` folder. If
you cannot, you are a level too high or too low. On Windows a ZIP often unpacks into a
folder of the same name inside itself, so you may need one more `cd 202609_workshop_GSCN`.

## Step 4: create the environment and the kernel

Run these three, one at a time, waiting for each to finish:

```
conda env create -f environment.yml
conda activate scverse-workshop
python -m ipykernel install --user --name scverse-workshop
```

The first one downloads about 2 GB and takes 10 to 30 minutes. It prints a lot, then goes
quiet at a line saying `Installing pip dependencies` for several minutes with nothing
visible happening. That is the slow part and it has not hung, so leave it alone. You are
done when your prompt comes back.

After `conda activate`, your prompt starts with `(scverse-workshop)` instead of `(base)`.
That is how you tell which environment you are in.

The third command registers the environment as a Jupyter kernel so you can select it
inside a notebook.

### Check

```
python -c "import scanpy, cellrank, palantir, pertpy, spatialdata, squidpy, cellcharter; print('setup ok')"
```

The first run takes a few minutes while the libraries build their caches, and it is fast
after that. If it prints `setup ok`, the software side is done. If it prints an error,
copy the whole message, not only the last line, and post it on
[Zulip](https://scverse.zulipchat.com/#narrow/channel/630708-2026-09.3A-Workshop-GSCN)
with your operating system.

## Step 5: download the data

Three files. Please download these in advance on a connection you trust. They come to
about 1 GB, and forty laptops pulling that over conference wifi at once will not go well.

- [Visium](https://s3.embl.de/spatialdata/raw_data/workshop/visium_2.1.0_2_io_subset.zip), 66 MB
- [Visium HD](https://s3.embl.de/spatialdata/raw_data/workshop/visium_hd_3.0.0_io_subset.zip), 228 MB
- [Xenium](https://s3.embl.de/spatialdata/raw_data/workshop/xenium_2.0.0_io_subset.zip), 786 MB

Unzip all three into `notebooks/day_2/spatialdata/data/` inside the materials folder. You
should end up with three folders in there:

```
visium_2.1.0_2_io_subset
visium_hd_3.0.0_io_subset
xenium_2.0.0_io_subset
```

Leave them as they are. The first notebook of the afternoon converts them into the
SpatialData Zarr format.

The day 1 datasets are much smaller and we will post them on Zulip shortly before the
workshop.

## Starting Jupyter

Every time you sit down to work:

```
conda activate scverse-workshop
cd <the materials folder>
jupyter lab
```

JupyterLab opens in your browser. Open a notebook and check the top right corner. It has
to say **scverse-workshop**. If it says `Python 3`, `base` or anything else, click it and
pick *scverse-workshop*, otherwise none of the packages will be there.

Starting JupyterLab from Anaconda Navigator works too. The kernel is registered for your
user account rather than for one environment, so *scverse-workshop* shows up in the
kernel list either way. What matters is picking the right kernel, not how you started
Jupyter.

## Troubleshooting

**Your prompt does not say `(base)`, or the shell does not recognise `conda`.**
On Windows you are probably in the ordinary Command Prompt or PowerShell. Use the
Anaconda Prompt from the Start menu. On macOS or Linux, close the terminal and open a new
one, since the installer only affects terminals started after it ran.

**`conda activate` tells you to run `conda init` first.**
Run `conda init`, then close the terminal completely and open a new one. On Windows
PowerShell, use `conda init powershell`.

**`conda env create` fails partway through.**
Usually a dropped connection or a full disk. Delete the half-built environment and start
over, nothing is lost:

```
conda env remove -n scverse-workshop
conda env create -f environment.yml
```

**"Solving environment" takes a very long time.**
A few minutes is normal. Much longer usually means an old conda, so run
`conda update -n base conda` and try again.

**Jupyter starts but the kernel is missing or keeps dying.**
Check that the third command in step 4 ran while `scverse-workshop` was active. Run
`jupyter kernelspec list` to see what Jupyter knows about, and `scverse-workshop` should
be in there. Running that install command again does no harm.

**Anything else.** Post it on
[Zulip](https://scverse.zulipchat.com/#narrow/channel/630708-2026-09.3A-Workshop-GSCN)
with your operating system, what you ran, and the full error text. We will pick it up
there, and otherwise sort it out in the setup hour on day 1.
