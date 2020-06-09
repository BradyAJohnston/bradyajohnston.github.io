---
title: Praise for pdb-tools
subtitle: Swiss army knife for molecular structures.
tags: python, structural biology, bash
---

# I just want to change one column.

An output from some MD work left me with a .pdb file with 0 _b-factors_.
```bash
brady@bmac 1 % tail modifed.pdb
ATOM   9670  CB  ALA   609     139.230  39.040  82.350  1.00  0.00
ATOM   9674  C   ALA   609     141.480  39.340  81.290  1.00  0.00
ATOM   9675  O   ALA   609     142.160  39.960  82.160  1.00  0.00
ATOM   9676  N   GLY   610     142.090  38.490  80.480  1.00  0.00
ATOM   9678  CA  GLY   610     143.490  38.100  80.430  1.00  0.00
ATOM   9681  C   GLY   610     144.370  38.940  79.520  1.00  0.00
ATOM   9682  O   GLY   610     144.650  40.130  79.960  1.00  0.00
ATOM   9683  OXT GLY   610     145.010  38.410  78.550  1.00  0.00
TER
ENDMDL
```

All I wanted was to quickly change them all to 1.00, so that I could move on to the next stage.

## `pdb-tools` to the rescue

A collection of simple scripts, written in python and available through the command line. Look at the full documentation [here](http://www.bonvinlab.org/pdb-tools/#list-of-tools).

The solution was fairly simple:
```bash
pdb_b -1.00 PPR_path_heavy.pdb > modified.pdb
```

Which gave the result:
```bash
brady@bmac 1 % tail modified.pdb
ATOM   9670  CB  ALA   609     139.230  39.040  82.350  1.00  1.00
ATOM   9674  C   ALA   609     141.480  39.340  81.290  1.00  1.00
ATOM   9675  O   ALA   609     142.160  39.960  82.160  1.00  1.00
ATOM   9676  N   GLY   610     142.090  38.490  80.480  1.00  1.00
ATOM   9678  CA  GLY   610     143.490  38.100  80.430  1.00  1.00
ATOM   9681  C   GLY   610     144.370  38.940  79.520  1.00  1.00
ATOM   9682  O   GLY   610     144.650  40.130  79.960  1.00  1.00
ATOM   9683  OXT GLY   610     145.010  38.410  78.550  1.00  1.00
TER
ENDMDL
```

And that was it! easy done. Will definitely be using these a lot more in the future.

Thanks so much to the team behind it [Rodrigues, J. P. G. L. M., Teixeira, J. M. C., Trellet, M. & Bonvin, A. M. J. J.](https://www.biorxiv.org/content/10.1101/483305v1.article-info)
