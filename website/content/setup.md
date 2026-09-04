+++
title = "Before you arrive"
[build]
  render = "never"
  list = "never"
+++

Please do this **before** day 1. The session at 11:00 on Monday is for troubleshooting what
did not work, not for installing from scratch on conference wifi.

### 1. Install the environments

We use two `conda` environments to avoid dependency conflicts. Both register a Jupyter
kernel, so you can switch between them from within JupyterLab.

```bash
# general single-cell (day 1 and day 2 morning)
conda create -y --name workshop_2026 python=3.10
conda activate workshop_2026
pip install jupyterlab notebook
conda install -y ipykernel conda-forge::python-annoy
pip install scikit-misc PhenoGraph celltypist palantir scrublet cellrank pydeseq2 \
    liana gseapy rpy2 anndata2ri scanpy python-igraph pyscipopt decoupler pybiomart adjustText
python -m ipykernel install --user --name workshop_2026
```

```bash
# spatial (day 2 afternoon)
conda create -y --name workshop_2026_spatial python=3.12
conda activate workshop_2026_spatial
pip install jupyterlab notebook
pip install spatialdata spatialdata-io spatialdata-plot napari-spatialdata squidpy pyproj
conda install -y ipykernel
python -m ipykernel install --user --name workshop_2026_spatial
```

Check that the install worked by starting JupyterLab and running `import scanpy` in the
`workshop_2026` kernel and `import spatialdata` in the `workshop_2026_spatial` kernel.

### 2. Download the data

The spatial datasets are large - please download them at home, not at the venue.

- [Visium](https://s3.embl.de/spatialdata/raw_data/workshop/visium_2.1.0_2_io_subset.zip) (~67 MB)
- [Visium HD](https://s3.embl.de/spatialdata/raw_data/workshop/visium_hd_3.0.0_io_subset.zip) (~228 MB)
- [Xenium](https://s3.embl.de/spatialdata/raw_data/workshop/xenium_2.0.0_io_subset.zip) (~786 MB)

The single-cell datasets for day 1 are smaller and will be shared in the materials
repository and on Zulip shortly before the workshop.

### 3. Join Zulip

Questions before, during and after the workshop go to the scverse Zulip. It is also where
we post data links and fixes during the sessions.
