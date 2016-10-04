## QAP BIDS Application

### Documentation
Extensive information can be found in the [Quality Assessment Protocol](http://preprocessed-connectomes-project.org/quality-assessment-protocol/) webpage.

### Description
Various objective measures for MRI data quality have been proposed over the years. However, until now no software has allowed researchers to obtain all these measures in the same place with relative ease. The [Quality Assessment Protocol](http://preprocessed-connectomes-project.org/quality-assessment-protocol/) package allows you to obtain spatial and anatomical data quality measures for your own data. Reports can optionally be generated that provide a variety of data visualizations to aid with quality assessment. 

This container calculates dataset level quality assessment metrics of structural and functional MRI data when run in "participant" mode and compiles the outputs of many different participants outputs into single CSV files when run in "group" mode.



### Usage
This App has the following command line arguments:

    usage: run.py [-h]
                  [--participant_label PARTICIPANT_LABEL [PARTICIPANT_LABEL ...]]
                  [--pipeline_file PIPELINE_FILE] [--n_cpus N_CPUS]
                  [--save_working_dir] [--group_level_report]
                  bids_dir output_dir

    PCP-QAP Pipeline Runner

    positional arguments:
      bids_dir              The directory with the input dataset formatted
                            according to the BIDS standard.
                            
      output_dir            The directory where the output CSV files should be
                            stored.

      {participant,group}   Level of the analysis that will be performed. Multiple
                            participant level analyses can be run independently
                            (in parallel). Group level analysis compiles the 
                            participant level quality metrics into group-level
                            csv files.
                            
    optional arguments:
      -h, --help            show this help message and exit
      
      --participant_label PARTICIPANT_LABEL [PARTICIPANT_LABEL ...]
                            The label of the participant that should be analyzed.
                            The label corresponds to sub-<participant_label> from
                            the BIDS spec (so it does not include "sub-"). If this
                            parameter is not provided all subjects should be
                            analyzed. Multiple participants can be specified with
                            a space separated list.
                            
      --pipeline_file PIPELINE_FILE
                            Name for the pipeline configuration file to use, uses
                            a default configuration if not specified
                            
                             
      --n_cpus N_CPUS       Number of execution resources available for the
                            pipeline, default=1
                            
      --mem                 Amount of RAM available to the pipeline in GB
                            default="6"
                                                        
      --save_working_dir    Save the contents of the working directory.
      
      --report              Generates pdf for graphically assessing data quality.



To run it in participant level mode (for one participant):

    docker run -i --rm \
        -v /Users/filo/data/ds005:/bids_dataset \
        -v /Users/filo/outputs:/outputs \
        bids-apps/qap:v1.0.0 \
        /bids_dataset /outputs --participant_label 01 participant


To run all subjects and generate the group level analysis report:

    docker run -i --rm \
        -v /Users/filo/data/ds005:/bids_dataset \
        -v /Users/filo/outputs:/outputs \
        bids-apps/qap:v1.0.0 \
        /bids_dataset /outputs group