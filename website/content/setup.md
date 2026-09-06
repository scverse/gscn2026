+++
title = "Technical setup"
subtitle = "Install this before day 1 — it takes about half an hour, most of it unattended."
+++

Everything in this workshop runs **on your own laptop**: one Anaconda environment,
one Jupyter kernel, the same for both days. Monday opens with a troubleshooting hour
from 12:00 to 13:00, but that hour is for fixing what did not work — not for
installing from scratch over conference wifi.

Five steps, in order, each ending with a check — so you always know whether to carry on
or to ask for help.

<!--more-->

You will need roughly **5 GB of free disk space** and a reasonable internet connection.
The environment itself is about 2 GB, the workshop data about 1 GB.

## Step 1 — Install Anaconda

Anaconda gives you Python plus the `conda` command we use to build the environment.
If you already have a working conda (Anaconda, Miniconda or Miniforge), skip to step 2 —
any of them works.

Download it from **[anaconda.com/download](https://www.anaconda.com/download)**. The
site asks you to register; you can also skip that from the link below the form.

### Windows

Follow the [official Windows guide](https://www.anaconda.com/docs/getting-started/anaconda/install/windows-gui-install)
and take the **64-Bit Graphical Installer**. Three choices in the installer matter:

1. **Just Me (recommended)** — installing for all users needs administrator rights and
   causes permission problems later.
2. **Install location** — accept the default. If you change it, pick a path with **no
   spaces and no special characters**.
3. **Do not** tick "Add Anaconda3 to my PATH environment variable". It is unticked by
   default and Anaconda recommends leaving it that way; you will use the Anaconda Prompt
   instead.

### macOS

Follow the [official macOS guide](https://www.anaconda.com/docs/getting-started/anaconda/install/mac-gui-install)
and take the **Graphical Installer**. Apple silicon (M1–M4) and Intel Macs need different
installers — the download page detects this for you. Intel Macs are no longer built for
new releases, so on an older Intel machine take the newest archived version from
[repo.anaconda.com/archive](https://repo.anaconda.com/archive/).

Accept the default install location. The installer sets up your shell for you.

### Linux

Follow the [official Linux guide](https://www.anaconda.com/docs/getting-started/anaconda/install/linux-install).
Download the `.sh` installer, then run it and answer `yes` when it offers to initialise
your shell:

```
bash ~/Downloads/Anaconda3-*-Linux-x86_64.sh
```

### Check

Open a fresh terminal — on **Windows**, search the Start menu for **Anaconda Prompt**
and open that, not the normal Command Prompt or PowerShell. On **macOS** open
**Terminal**, on **Linux** your usual terminal.

The line where you type should begin with `(base)`:

```
(base) C:\Users\yourname>
```

Then run:

```
conda --version
```

You should see something like `conda 25.x.x`. If the prompt does not say `(base)`, or
`conda` is "not recognised", jump to [Troubleshooting](#troubleshooting) below.

## Step 2 — Download the workshop materials

The notebooks and the environment file live in the
[materials repository](https://github.com/scverse/202609_workshop_GSCN).

If you use git:

```
git clone https://github.com/scverse/202609_workshop_GSCN.git
```

If you do not, open the [repository](https://github.com/scverse/202609_workshop_GSCN) in your browser, click
the green **Code** button, choose **Download ZIP**, and unzip it somewhere you can find
again — your Desktop or Documents folder is fine. Avoid a path with spaces or umlauts if
you can, and do not leave it inside the Downloads folder on Windows, where the unzipped
copy is easy to lose.

## Step 3 — Move into that folder

This is the step people most often get wrong, so it has its own section. In your terminal
you have to be **inside the folder you just downloaded** before the next commands work.

Type `cd ` — that is `cd` followed by a space — and then get the folder path in:

- **Windows:** find the folder in File Explorer, hold **Shift** and right-click it, choose
  **Copy as path**, then paste into the Anaconda Prompt with a right-click.
- **macOS:** drag the folder from Finder onto the Terminal window and the path appears.
- **Linux:** most file managers have "Open in Terminal" on right-click, which skips this
  step entirely.

Press Enter. Then list what is around you:

```
dir          (Windows)
ls           (macOS and Linux)
```

You are in the right folder if the output contains **`environment.yml`** and a
**`notebooks`** folder. If it does not, you are one level too high or too low — on
Windows the ZIP often unpacks into a folder of the same name inside itself, so you may
need one more `cd 202609_workshop_GSCN`.

## Step 4 — Create the environment and the kernel

Still in that folder, run these three commands one at a time, waiting for each to finish:

```
conda env create -f environment.yml
conda activate scverse-workshop
python -m ipykernel install --user --name scverse-workshop
```

The first one downloads about 2 GB and takes **10–30 minutes** depending on your
connection. It prints a lot; that is normal. It is finished when your prompt comes back.

After `conda activate`, the start of your prompt changes from `(base)` to
`(scverse-workshop)`. That is how you can always tell which environment you are in.

The third command registers the environment as a Jupyter kernel, so you can pick it from
inside a notebook.

### Check

```
python -c "import scanpy, cellrank, palantir, pertpy, spatialdata, squidpy, cellcharter; print('setup ok')"
```

If this prints `setup ok`, you are done with the software. If it prints an error, copy the
**whole** message — the last line alone is rarely enough — and post it on
[Zulip](https://scverse.zulipchat.com/#narrow/channel/630708-2026-09.3A-Workshop-GSCN) with your operating system.

## Step 5 — Download the data

Three files, please download them at home:

- [Visium](https://s3.embl.de/spatialdata/raw_data/workshop/visium_2.1.0_2_io_subset.zip) — 66 MB
- [Visium HD](https://s3.embl.de/spatialdata/raw_data/workshop/visium_hd_3.0.0_io_subset.zip) — 228 MB
- [Xenium](https://s3.embl.de/spatialdata/raw_data/workshop/xenium_2.0.0_io_subset.zip) — 786 MB

Unzip all three into `notebooks/day_2/spatialdata/data/` inside the materials folder. You
should end up with three folders in there:

```
visium_2.1.0_2_io_subset
visium_hd_3.0.0_io_subset
xenium_2.0.0_io_subset
```

Leave them as they are — the first notebook of the afternoon converts them into the
SpatialData Zarr format itself.

The day 1 datasets are much smaller and will be announced on Zulip shortly before the
workshop.

## On the day: starting Jupyter

Every time you sit down to work, three things in this order:

```
conda activate scverse-workshop
cd <the materials folder>
jupyter lab
```

JupyterLab opens in your browser. Open any notebook and look at the **top right corner**:
it must say **scverse-workshop**. If it says `Python 3`, `base` or anything else, click
it and choose *scverse-workshop* — otherwise none of the packages will be found.

## Troubleshooting

**The prompt does not say `(base)`, or `conda` is not recognised.**
On Windows you are probably in the normal Command Prompt or PowerShell. Use the
**Anaconda Prompt** from the Start menu instead. On macOS or Linux, close the terminal
and open a new one — the installer only affects terminals started after it ran.

**`conda activate` says you must run `conda init` first.**
Run `conda init`, then close the terminal completely and open a new one. On Windows
PowerShell specifically, `conda init powershell` is the one you want.

**`conda env create` fails partway through.**
Usually a dropped connection or a full disk. Delete the half-built environment and start
again — nothing is lost:

```
conda env remove -n scverse-workshop
conda env create -f environment.yml
```

**"Solving environment" runs for a very long time.**
Anything up to a few minutes is normal. Much longer usually means an older conda; update
it with `conda update -n base conda` and try again.

**Jupyter opens but the kernel is missing or keeps dying.**
Check that step 4's third command ran while `scverse-workshop` was active. You can list
what Jupyter knows about with `jupyter kernelspec list`; `scverse-workshop` should appear.
Re-running that command is harmless.

**Anything else.** Post it on [Zulip](https://scverse.zulipchat.com/#narrow/channel/630708-2026-09.3A-Workshop-GSCN) — operating system, what
you ran, and the full error text. Someone will get back to you before Monday, and we keep
the troubleshooting hour on day 1 for whatever is left.
