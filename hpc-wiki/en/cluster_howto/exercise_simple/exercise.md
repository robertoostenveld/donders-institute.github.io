# Exercise: simple batch job

The aim of this exercise is to get you familiar with the torque client tools for submitting and managing cluster jobs. We will firstly create a script that calls the `sleep` command for a given period of time.  After that, we are going to submit the script as jobs to the cluster.

## Tasks

1. make a script called `run_sleep.sh` with the following content:

    ```bash
    #!/bin/bash
    
    my_host=$( /bin/hostname )
    
    time=$( date )
    echo "$time: $my_host falls asleep ..."
    
    sleep $1
    
    time=$( date )
    echo "$time: $my_host wakes up."
    ``` 

2. make sure the script runs locally

    ```bash
    $ chmod +x run_sleep.sh
    $ ./run_sleep.sh 1
    Mon Sep 28 16:36:28 CEST 2015: dccn-c007.dccn.nl falls asleep ...
    Mon Sep 28 16:36:29 CEST 2015: dccn-c007.dccn.nl wakes up.
    ```

3. submit a job to run the script

    ```bash
    $ echo "$PWD/run_sleep.sh 60" | qsub -N 'sleep_1m' -l 'procs=1,mem=10mb,walltime=00:01:30'
    6928945.dccn-l029.dccn.nl
    ```

4. check the job status.  For example,

    ```bash
    $ qstat 6928945
    ```

    Attention: The torque job id given here should be replaced accordingly.

5. or monitor it until it is complete

    ```bash
    $ watch qstat 6928945
    ```

    Tip: the `watch` utility is used here to repeat the `qstat` command every 2 seconds. Press `Ctrl-c` to quit the `watch` program when the job is finished. 

6. examine the output file, e.g. `sleep_10.o6928945`, to find out the resource consumption of this job

   ```bash
   $ cat sleep_1m.o6928945 | grep 'Used resources'
   Used resources:	   cput=00:00:00,mem=4288kb,vmem=433992kb,walltime=00:01:00
   ```
7. submit another job to run the script, with longer duration of `sleep`.  For example,

    ```bash
    $ echo "$PWD/run_sleep.sh 3600" | qsub -N 'sleep_1h' -l 'procs=1,mem=10mb,walltime=01:10:00'
    6928946.dccn-l029.dccn.nl
    ```

    Note: Try to compare the command in step 3.  As we expect the job to run longer, the requirement on the job walltime is also extended to 1 hour 10 minutes.

8. Ok, we don't want to wait for the 1-hour job to finish. Let's cancel the job.  For example,

    ```bash
    $ qdel 6928946
    ```
