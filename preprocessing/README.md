# Pipeline for data preprocessing using `ccdops`

This file contains the general description of the data pipeline that we will use for the initial CCD reduction to prepare data for analysis, whether it be photometry or spectra extraction.

### Things to do:

Currently, it is a reduction pipeline focused on the way we prepare data for spectroscopic reduction. We should extend it to general reduction in the future by adding:

- biasing
- flat field reduction

Can extend this by, for example, adding flags at the start of the reduction notebook.

#### Data Cleanup

Need to include functionality for automatically recognising and assigning `IMAGETYP` based on the name of the files; currently we can only do it manually.

#### Data Reduction

Need to make sure we create master darks correctly with respect to the pixel-by-pixel averaging.

## Step One: Data Cleanup

This pipeline handles the whole data library using the `ccdproc` class `ImageFileCollection`. This allows us for quick filtering of images based on values in the header of each file. To be able to do this in the standardised way, we need to first make sure that all images conform to some simple criteria. We employ the Jupyter Notebook `data-cleanup.ipynb` for this task. This step can be skipped if the data already conforms to the requirements.

We need to make sure of two things:

- the header has a category named `'IMAGETYP'`, which specifies the type of image. We can choose between `['DARK', 'LIGHT', 'CALIB']` for the dark, science, and calibration lamp images respectively.
- the header has a category named `'BUNIT' = ADU`, which specifies the unit of signal in the images. This is needed so that images can be loaded as a `CCDData` type and the `ccdproc` functions can perform their operations.

You can find more information about how this is done [here](https://www.astropy.org/ccd-reduction-and-photometry-guide/v/dev/notebooks/01-11-reading-images.html).

### Specifying working directory

We begin by setting the working directories for:

- the raw data: we set this directory as the `data` directory
- the cleaned data: we set this directory as the `data-cleaned` directory.

Both of the above are in the same parent directory as our scripts. These values can be modified in the script.

### Performing the cleanup

The template provided takes a set of data from `data` by following a naming scheme, and records the copy with modified header to `data-cleaned` following a naming scheme. Currently, we have to manually provide the naming template, number of images, and type of image.

## Step Two: Data Reduction

This step of the process is done inside the notebook `pipeline-preproc.ipynb`. The pipeline loads the images with the filled headers as an `ImageFileCollection`. Then, we can separate the process in two main steps.

### Master dark creation

The notebook computes master darks using `ccdproc.combine()` and records the master darks in folder `data-reduced`. There are several ways to do the averaging of pixels. The current implemented one is the method given in the manual for `ccdproc` i.e. averaging of pixel values with sigma clipping for extreme values.

### Master dark subtraction

The notebook goes over all science and calibration images and subtracts the correct master dark based on the exposure time of the image. The subtracted images are once again saved in the `data-reduced` folder.
