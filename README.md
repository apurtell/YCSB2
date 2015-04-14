Yahoo! Cloud System Benchmark (YCSB)
====================================
[![Build Status](https://travis-ci.org/brianfrankcooper/YCSB.png?branch=master)](https://travis-ci.org/brianfrankcooper/YCSB)

Links
-----
http://wiki.github.com/brianfrankcooper/YCSB/  
http://research.yahoo.com/Web_Information_Management/YCSB/  
ycsb-users@yahoogroups.com  

Getting Started
---------------

1. Download the latest release of YCSB:

    ```sh
    wget https://github.com/downloads/brianfrankcooper/YCSB/ycsb-0.1.4.tar.gz
    tar xfvz ycsb-0.1.4
    cd ycsb-0.1.4
    ```
    
2. Set up a database to benchmark. There is a README file under each binding 
   directory.

3. Run YCSB command. 
    
    ```sh
    bin/ycsb load basic -P workloads/workloada
    bin/ycsb run basic -P workloads/workloada
    ```

  Running the `ycsb` command without any argument will print the usage. 
   
  See https://github.com/brianfrankcooper/YCSB/wiki/Running-a-Workload
  for a detailed documentation on how to run a workload.

  See https://github.com/brianfrankcooper/YCSB/wiki/Core-Properties for 
  the list of available workload properties.


Using HdrHistogram to correct for coordinated omission effects
====================================

This version includes a new Measurement option for recording latencies with
[HdrHistogram](https://github.com/HdrHistogram/HdrHistogram). Use

    -p measurementtype=hdrhistogram

Or, the combined measurement option allowing old and new measurement side by side:

    -p measurementtype=hdrhistogram+histogram

The HdrHistogram measurement type supports optional logging of HdrHistogram data to a file.
Control this with

    -p hdrhistogram.fileoutput=<true|false>

and

    -p hdrhistogram.output.path=<path>

The [HistogramLogProcessor](https://github.com/HdrHistogram/HdrHistogram/blob/master/HistogramLogProcessor) script provided with HdrHistogram can process the files (you need to copy the HdrHistogram.jar into the script folder first) into .hgrm files that can be plotted with [plotFiles](https://github.com/HdrHistogram/HdrHistogram/blob/master/GoogleChartsExample/plotFiles.html) to graph latency by percentile distribution.

(Source: [psy-lob-saw](http://psy-lob-saw.blogspot.co.at/2015/03/fixing-ycsb-coordinated-omission.html))
