# Example LSF script submissions

LSF (Load Sharing Facility) at Sanger Institute.


# How to submit?

All scripts are written bash scripts with `#BSUB` notation. To submit them as jobs use the following command:

```
bsub < myjob.lsf
```

## Converting to bsub inline command

Just copy the options for `#BSUB` tags from the file to an inline command.

For example:
```
#!/bin/bash
#BSUB -q normal                                     # name of the queue gpu-lotfollahi
#BSUB -M 8G                                         # 8G RAM memory
#BSUB -R "select[mem>8G] rusage[mem=8G]"            # same as above
#BSUB -o logs/%J.out                                # output file
#BSUB -e logs/%J.err                                # error file
#BSUB -n 4                                          # number of cores in total

[code here]
```

Turns to
```
bsub -q normal \
    -M 8G -R "select[mem>8G] rusage[mem=8G]" \
    -o logs/%J.out \
    -e logs/%J.err \
    -n 4 \
    /path/to/your/script.sh
```

Where `[code here]` is placed inside `/path/to/your/script.sh`