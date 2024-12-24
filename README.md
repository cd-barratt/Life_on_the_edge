Full tutorials for setup and running the LotE toolbox - https://cd-barratt.github.io/Life_on_the_edge.github.io/Vignette

This software is intended for HPC use. Please make sure the software below is installed and functional in your HPC environment before proceeding:

Life on the edge data and scripts (data: https://datadryad.org/stash/dataset/doi:10.5061/dryad.2rbnzs7t4, scripts also available here: https://zenodo.org/records/13643383)
Singularity (3.5) and bioconductor container with correct R version: https://cloud.sylabs.io/library/sinwood/bioconductor/bioconductor_3.14
R (4.1.3). Dependencies for toolbox installed within R version in singularity container upon setup (you specify your R libraries in the script where annotated)
Julia (1.7.2)
Additionally you need to download the following and place in the correct directories to be sure the toolbox will function properly:

* Environmental predictor data - please download and place environmental layers used for SDMs, GEAs etc in separate folders for current and future environmental conditions. These folders can be named/specified exactly in the params.tsv file ('current_climate_data_path', 'future_climate_data_path'). We generally use climate projections for all 19 bioclim variables [Worldclim2](https://www.worldclim.org/data/index.html) as well as landcover [Globio4](https://www.globio.info/globio-data-downloads]) and slope (calculated from a digital elevation model available with Worldclim2 data). For future conditions you must select a GCM and time period (e.g. time period: 2061-2080, Global circulation model: HadGEM3-GC31-LL). Each time you rin the toolbox for a given species the data will be clipped to the study region for your analyses (extents can be controlled per species using the 'geographic_extent' parameter in params.tsv)

* Plink and Maxent executables - please download a working executable for Maxent, [maxent.jar](https://biodiversityinformatics.amnh.org/open_source/maxent/) as well as a working [plink](https://www.cog-genomics.org/plink/) executable. These can be placed anywhere (we recommend within -data-), and the toolbox locates these with the 'maxent_executable' and 'plink_executable' parameters in Params.tsv

* Country border data - please download a world shapefile and unzip it to this directory (e.g. [Natural Earth country borders](https://www.naturalearthdata.com/http//www.naturalearthdata.com/download/50m/cultural/ne_50m_admin_0_countries.zip))

To use the toolbox, make a working directory in your HPC environment (e.g. ~/work/Life_on_the_edge_pipeline/) and move or copy the Singularity container there. Download the scripts and R functions from the attached Zenodo repository and have them all in the same file structure as your Life_on_the_edge working directory.

i.e. so your working directory should contain the following:

-data-
-scripts-
-outputs-
bioconductor_3.14.sif
Params.tsv
R_functions

To make things as clean as possible, you may wish to make a submit scripts directory (e.g. ~/submit_scripts/Life_on_the_edge_pipeline), and a data directory (e.g. ~/data/Life_on_the_edge_pipeline). I would suggest you unzip and move the contents of Life_on_the_edge_submit_scripts.zip to your submit scripts directory and use your data directory for storing raw (unprocessed) genomic data.

Before you begin there will be some setup needed. All scripts will need modification to point towards your work directory (
YOUR_SUBMIT_SCRIPTS_DIR) and data (
YOUR_EMAIL). Paths to your own local R libraries, Singularity and Julia will differ from the example based on your own HPC setup, so these will need to be edited to match your own structure.

The same goes for the params.tsv file which controls the analyses, the paths in this will need to be modified ($YOUR_WORKING_DIR).
00_process_environmental_data - a script to strip out multi-band environmental layers (i.e. Wordlclim2 data) and store them for use with Life on the edge
