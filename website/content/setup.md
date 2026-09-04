+++
title = "Before you arrive"
[build]
  render = "never"
  list = "never"
+++

Please install the software **before** day 1. Monday has a dedicated troubleshooting
hour from 12:00 to 13:00, but it is meant for fixing what did not work, not for
installing from scratch over conference wifi.

The commands below are identical on macOS, Windows and Linux. Run them in the
**Anaconda Prompt** on Windows, or a normal terminal on macOS and Linux.

### 1. Create the two environments

We use two environments so that the spatial packages cannot conflict with the rest. Both
register a Jupyter kernel, so you can switch between them inside JupyterLab.

```
conda create -y -n workshop_2026 python=3.11
conda activate workshop_2026
pip install jupyterlab notebook ipykernel scanpy anndata scikit-misc leidenalg igraph scrublet decoupler pydeseq2 adjustText palantir cellrank scanorama scib-metrics liana pertpy lamindb seaborn filelock "statsmodels<0.15"
python -m ipykernel install --user --name workshop_2026
```

```
conda create -y -n workshop_2026_spatial python=3.11
conda activate workshop_2026_spatial
pip install jupyterlab notebook ipykernel spatialdata spatialdata-io spatialdata-plot "napari[all]" napari-spatialdata squidpy cellcharter scvi-tools pyproj
python -m ipykernel install --user --name workshop_2026_spatial
```

Keep the quotes around `"statsmodels<0.15"` and `"napari[all]"` - without them the
Windows command prompt reads `<` as a redirect and zsh on macOS tries to expand `[all]`.

If you do not have conda, install
[Miniforge](https://github.com/conda-forge/miniforge#download) first. A plain
`python -m venv` works too - only the activate command differs.

These package lists were installed and imported end to end on Python 3.11 on 2026-09-04,
and also resolve cleanly for Linux and Windows. They are kept in the repository as
[requirements-general.txt](https://github.com/scverse/gscn2026/blob/main/env/requirements-general.txt)
and [requirements-spatial.txt](https://github.com/scverse/gscn2026/blob/main/env/requirements-spatial.txt).

### 2. Check that it worked

```
conda activate workshop_2026
python -c "import scanpy, cellrank, palantir, pertpy; print('day 1 ok')"
conda activate workshop_2026_spatial
python -c "import spatialdata, squidpy, cellcharter, napari_spatialdata; print('day 2 ok')"
```

If either line prints an error, post it in the Zulip channel **before** Monday and we will
sort it out there. Include your operating system and the full error message.

### 3. Download the data

Large files - please download at home, not at the venue. All three are direct downloads.

- [Visium](https://s3.embl.de/spatialdata/raw_data/workshop/visium_2.1.0_2_io_subset.zip) - 66 MB
- [Visium HD](https://s3.embl.de/spatialdata/raw_data/workshop/visium_hd_3.0.0_io_subset.zip) - 228 MB
- [Xenium](https://s3.embl.de/spatialdata/raw_data/workshop/xenium_2.0.0_io_subset.zip) - 786 MB

The day 1 single-cell datasets are much smaller and will be posted in the materials
repository and on Zulip shortly before the workshop.

### 4. Join the Zulip channel

Questions before, during and after the workshop go to the **2026-09: Workshop GSCN**
channel on the scverse Zulip. It is also where we post data links and fixes as the
sessions run, so please join it before Monday.
