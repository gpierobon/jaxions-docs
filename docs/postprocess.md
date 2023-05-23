---
layout: default
title: Python tools
nav_order: 5
---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## The `pyaxions` library

In the `scripts/pyaxions` folder several python modules are facilitating the visualisation and analysis of data. We briefly describe some of the most useful tools.

- `jaxions.py`
- `spectrum.py`
- `simgen.py`
- `specfromF.py`

```python
import sys
sys.path.append('path/to/jaxionsdir/jaxions/scripts/')
from pyaxions import jaxions as pa
```

## Checking the parameters
{: #checkp}

An auxiliary tool to check whether the chosen simulation parameters are physically adequate can be found in `scripts/params.py`. It includes the follwing parameters:

- `--n`: power-law index $$ n $$ in the axion mass growth, $$ m_a\propto T^{-n/2}$$
- `--N`: resolution of the lattice in each dimension
- `--L`: physical size of the lattice in units of $$ L_1 $$ 
- `--msa`: the inverse size of the string core 
- `--zf`: the final simulation time (normalised conformal time) 
- `--kref`: select a mode to study,  in units of $$ L_1^{-1} $$

```
python3 params.py --n 7.0 --N 4096 --L 6 --msa 1.5 --zf 4.0 --kref 10.0
```

Under construction ...
