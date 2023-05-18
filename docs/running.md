---
layout: default
title: Running the code
nav_order: 4
---

Under construction ...

## Example scripts

```bash
N=256 ; RANKS=4 ; DEPTH=$(echo $N/$RANKS | bc)
GRID=" --size $N --depth $DEPTH --zgrid $RANKS"

LOW=" --lowmem" ; PREC=" --prec single" ; DEVI=" --device cpu"
PROP=" --prop rkn4" ; SPEC=" --spec"

STEP=20000 ; WDZ=1.0 ; SST0=10 ; LAP=1
SIMU=" $PREC $DEVI $PROP --steps $STEP --wDz $WDZ --sst0 $SST0 --lap $LAP"

QCD=4.0 ; MSA=1.00 ; L=6.0 ; ZEN=4.0 ;
PHYS="--qcd $QCD --msa $MSA --lsize $L --zf $ZEN $XTR"

INCO=" --ctype smooth --kcr 1.1 --sIter 5 "

DUMP=10 ; WTIM=1.0 ;
MEAS=$(echo 1+2+4+8+32+128+65536+16384 | bc )
SPMA=$(echo 1 | bc )
SKGV=$(echo 1 | bc )
OUTP="--dump $DUMP --meas $MEAS ---spmask $SPMA --spKGV $SKGV --nologmpi --wTime $WTIM "
export OMP_NUM_THREADS=4

mpirun $USA -np $RANKS vaxion3d $GRID $SIMU $PHYS $INCO $OUTP
```
