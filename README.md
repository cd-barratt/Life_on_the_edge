# Life on the edge: a new toolbox for population-level climate change vulnerability assessments
---

Dataset contains all input files needed to run Life on the edge for an example dataset (Afrixalus fornasini)
You may run data for your focal species following the structure and content of the example files provided


## Description of the data and file structure

* Params.tsv is a tab separated file that contains all parameters for running each species dataset. The parameters are already set to default values for the example dataset to replicate results in the manuscript


-data- directory:
/genomic_data/
* Input genomic files are pre-processed and stored in the species directory in './-data-/genomic_data' (Plink formatted .map and .ped files)
* denovo_test_parameter_ranges.csv is for optimizing parameters for Stacks with new datasets (not necessary in the example as it is already processed)

/spatial_data/
* Input georeferenced coordinates for each sample are in a .csv file in the species directory in './-data-/spatial_data'

/environmental_data/
* Within a folder named '30s' (the spatial resolution of the data), there are climate projections for all 19 bioclim variables as well as landcover and slope
* These projections are from the Worldclim2 (https://www.worldclim.org/data/index.html) dataset, and provided for current and future (time period: 2061-2080, Global circulation model: HadGEM3-GC31-LL) conditions

/map_data/
* Contains 5 files that constitute the world shapefile used for mapping (from https://www.naturalearthdata.com/)

* A working maxent.jar (https://biodiversityinformatics.amnh.org/open_source/maxent/) file is provided as well as a working plink (https://www.cog-genomics.org/plink/) version


-outputs- directory:
* An empty folder that will be populated with results when running Life on the edge. The log files will also be stored here.



## Sharing/Access information

Links to other publicly accessible locations of the data: 
* https://github.com/cd-barratt/Life_on_the_edge


Data was derived from the following sources:
* Raw sequence data is available at the European Nucleotide Archive (ENA): Myotis escalerai and M. crypticus (PRJEB29086), and the NCBI Short Read Archive (SRA): Afrixalus fornasini – (SRP150605). 
* Spatial occurrence data was derived from the respective publications https://doi.org/10.1111/mec.14862 and https://doi.org/10.1073/pnas.1820663116

## Code/Software

HPC submission scripts are located in Life_on_the_edge_submit_scripts.zip:
* 00_setup_life_on_the_edge.sh - initial setup script for Life on the edge
* 01_run_life_on_the_edge.sh - a script that calls all relevqant scripts and functions to run the toolbox in its entirety
* -run_life_on_the_edge-.sh - a wrapper script whereby multi-species or different parameter sets for analyses may be conducted as separate jobs via HPC

Life on the edge scripts and R functions are located in Life_on_the_edge_pipeline_scripts_functions.zip

R_functions directory:
* life_on_the_edge_functions.R - contains all functions that make up the Life on the edge toolbox

-scripts- directory:
* -LFMM-.R - an R script to run LFMM analyses (recommended as some systems sometimes cause crashes when using the gea_lfmm() function in the life_on_the_edge_functions.R file)
* run_LOE_exposure.R - runs all functions to prepare data and quantify exposure for each population
* run_LOE_population_vulnerability.R - runs all functions to quantify population vulnerability for each population and create summary PDFs 
* run_LOE_range_shift_potential.R - runs all functions to quantify range shift potential for each population
* run_LOE_sensitivity.R - runs all functions to quantify sensitivity for each population

processing_environmental_data directory:
00_process_environmental_data - a script to strip out multi-band environmental layers (i.e. Wordlclim2 data) and store them for use with Life on the edge

processing_genomic_data_directory:
* -batch_extract_results-.sh - wrapper script to extract all results for parameter combination optimisation in Stacks. Batch calls 02b_extract_results.sh
* -batch_test_denovo-.sh - wrapper script to run all parameter combinations of m, M and n in Stacks. Batch calls 02a_denovo_map_test.sh
* -download_SRA_accession-.sh wrapper script to download SRA accessions for multiple datasets. Batch calls 00b_download_SRA_data.sh
* 00a_download_ENA_data.sh - script to download specific datasets from ENA
* 00b_download_SRA_data.sh - script to download specific datasets from SRA
* 01_process_radtags.sh - script to demultiplex raw reads using the process_radtags program in Stacks
* 02a_denovo_map_test.sh - script to run each parameter combination of m, M and n in Stacks
* 02b_extract_results.sh - script to extract each result for parameter combination optimisation in Stacks
* 02c_plot_results.R - script to plot results of parameter optimisations in Stacks
* 03a_denovo_map_full.sh - Script to run the full denovo_map.pl program in Stacks based on the optimised parameters in the above script

