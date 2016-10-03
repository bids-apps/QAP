## QAP BIDS Application

Various objective measures for MRI data quality have been proposed over the years. However, until now no software has allowed researchers to obtain all these measures in the same place with relative ease. The [Quality Assessment Protocol](http://preprocessed-connectomes-project.org/quality-assessment-protocol/) package allows you to obtain spatial and anatomical data quality measures for your own data.


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
                            Name for the pipeline configuration file to use
      --n_cpus N_CPUS       Number of execution resources available for the
                            pipeline
      --save_working_dir    Save the contents of the working directory.
      --group_level_report  Generates a group level report pdf.



To run it in participant level mode (for one participant):

    docker run -i --rm \
        -v /Users/filo/data/ds005:/bids_dataset \
        -v /Users/filo/outputs:/outputs \
        bids-apps/qap:v1.0.0 \
        /bids_dataset /outputs --participant_label 01


To run all subjects and generate the group level analysis report:

    docker run -i --rm \
        -v /Users/filo/data/ds005:/bids_dataset \
        -v /Users/filo/outputs:/outputs \
        bids-apps/qap:v1.0.0 \
        --group_level_report \
        /bids_dataset /outputs 