# roost-dataset: remote sensing object detection dataset
We release multi-channel weather radar sensing datasets with roost annotations, 
for the purpose of **ecological analyses** and 
developing **visual object detection and tracking models** to recognize biological phenomena in radar data.

### Overview
Weather radar data hold information about biological phenomena in the atmosphere. 
This repository releases datasets each consisting of:
1. a json file that stores (1) information about a list of radar **scans** and
(b) **annotations** of roosts of flying animals; 
2. json files that store the **splitting** of the radar scan ids into training, validation, and testing sets 
for machine learning; 
3. npz files that save **arrays** rendered from radar products corresponding to the list of scans.

Shape and direction:
- Each npz file is a dictionary with array and dualpol_array as two keys.
  - array: a 3x5x600x600 array where the dimensions are 
    radar fields {reflectivity, velocity, spectrum_width}, 
    elevation angles {0.5, 1.5, 2.5, 3.5, 4.5} degrees,
    and 600x600 pixels representing a 300km x 300km region centered at a radar station.
  - dualpol_array: a 3x5x600x600 array where the radar fields 
    {differential_reflectivity, cross_correlation_ratio, differential_phase} 
    are available since around 2008.
- Arrays and annotations are both in the **geographical direction**. 
Large y indicates North (row 0 is South) and large x indicates East. 
- To visualize the array channels using matplotlib's `pyplot.imshow`, 
we need to set `origin='lower'` to get the **image direction** where the top of the image (row 0) is North.

### Release
The json files are available under **datasets**. 
- **roosts_v0.0.1_official** defines a toy mini-dataset to demonstrate the format of roosts_v0.1.0.
- **roosts_v0.1.0_official** defines a standardized dataset constructed by [1]. Data are originally labeled by [2].

The rendered arrays can be downloaded from **TODO**.

To reproduce these json files and render arrays yourself, please refer to 
[wsrdata](https://github.com/darkecology/wsrdata/tree/master).
These datasets can continue to be upgraded with more radar scans and annotations, .

### Visualization
You may follow the installation below and run `tools/visualization.ipynb` to visualize a scan and its annotations. 
The notebook allows you to render an array for a radar scan interactively, 
if you have not obtained rendered arrays already.

#### Installation
```bash
conda create -n ENV python=3.6 # replace ENV by your favorate name
conda activate ENV
pip install git+https://github.com/darkecology/pywsrlib#egg=wsrlib
```

Optional installation for running jupyter notebook on a server.
  ```bash
  pip install jupyter
  conda install -c anaconda ipykernel
  python -m ipykernel install --user --name=ENV # Add the python environment to jupyter
  ```
- Run jupyter notebook on a server: `jupyter notebook --no-browser --port=9999`
- Monitor from local: `ssh -N -f -L localhost:9998:localhost:9999 username@server`
- Enter `localhost:9998` from a local browser tab to run the jupyter notebook interactively;
  the notebook should be self-explanatory.


### References
[1] Perez, Gustavo, Wenlong Zhao, Zezhou Cheng, Maria Belotti, Yuting Deng, Victoria Simons, Elske Tielens, 
Jeffrey F. Kelly, Kyle G. Horton, Subhransu Maji, Daniel Sheldon. 
["Using spatio-temporal information in weather radar data to detect and track communal bird roosts."](https://www.biorxiv.org/content/10.1101/2022.10.28.513761v1.abstract) 
bioRxiv (2022): 2022-10.<br />
[2] Laughlin, Andrew J., Daniel R. Sheldon, David W. Winkler, and Caz M. Taylor. 
["Quantifying non‐breeding season occupancy patterns and the timing and drivers of autumn migration for a migratory songbird using Doppler radar."](https://onlinelibrary.wiley.com/doi/abs/10.1111/ecog.01988) 
Ecography 39, no. 10 (2016): 1017-1024.