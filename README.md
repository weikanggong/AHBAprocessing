# AHBAprocessing

This repository provides Matlab code for reproducing a range of analyses involving processing Allen Human Brain Atlas gene expression data and running a range of analyses to evaluate the effect of different processing choices.

Please read our paper, and if you use this code, please cite our paper:
A. Arnatkeviciute, B.D. Fulcher, A. Fornito. A practical guide to linking brain-wide gene expression and neuroimaging data.

NOTE: The code has been updated on the 28th August 2018 - in the previous version gene ordering in the ROI x gene matrices did not correspond to the gene information provided in the probeInformation structure.
Now this issue is fixed. If you processed the data before this date, please re-process it using the updated code.

Contact Aurina Arnatkeviciute by [email](mailto:aurina.arnatkeviciute@monash.edu).

### Dependencies:
[Brain Connectivity Toolbox](https://sites.google.com/site/bctnet/), Version 2017-15-01.
[Toolbox Fast Marching](https://au.mathworks.com/matlabcentral/fileexchange/6110-toolbox-fast-marching), Version 1.2.0.0

### Data files
Data files required for this project are hosted on [this figshare repository](https://doi.org/10.6084/m9.figshare.6852911).
Please create a directory called `data` in the root directory and download data there.

### Data processing
After retrieving data add relevant paths using `AddPaths.m`, data can be generated by running `processingPipeline.m` with selected options.
In order to calculate distances on the cortical surface, toolbox_fast_marching toolbox needs to be installed by running the following lines within matlab from the code/peripheralFunctions/toolbox_fast_marching directory:
* `mex -setup`
* `compile_mex`;

This script will run 4 data processing functions:
* `S1_extractData` - extracts the data from excel files and saves it in Matlab format
* `S2_probes` - performs probe selection and data filtering if required
* `S3_samples2parcellation` - assigns samples to the regions of interest in the parcellation
* `S4_normalisation` - performs data normalisation and calculates correlated gene expression and also provides data in the region x gene format.

See `README_processingPipeline.txt` for more information.

To generate data for all four parcellations using selected options use `processingPipeline_4parcellations.m`.

### Analysis
Figures in our paper can be regenerated using `makeFigures.m` in the `plotting` folder. All scripts should be run from the root directory. Other relevant analysis scripts are in `dataProcessing`.

### Example usage:
After downloading [data from figshare](https://doi.org/10.6084/m9.figshare.6852911) to the `data` directory, add the contents of the mater directory to the path using `AddPaths` function.

To enable distance calculation on the cortical surface, install `toolbox_fast_marching toolbox`.
To install the toolbox run the following lines within matlab from the `code/peripheralFunctions/toolbox_fast_marching` directory (for more information refer to [documentation](https://au.mathworks.com/matlabcentral/fileexchange/6110-toolbox-fast-marching)):
* `mex -setup`
* `compile_mex`;

```matlab
    % Add paths required for the project:
    AddPaths
    % go to the directory where toolbox is located
    cd code/peripheralFunctions/toolbox_fast_marching
    % install the toolbox_fast_marching
    mex -setup
    compile_mex
    % Generate ALL figures:
    makeFigures
    % Run all data processing scripts from scratch (with default options):
    processingPipeline
```
