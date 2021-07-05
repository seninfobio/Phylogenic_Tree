# Phylogentic_tree constructions

[Molecular dating and gene family evolution](https://www.protocols.io/view/chromosome-scale-genome-assembly-of-kiwifruit-acti-vgse3we?step=9)


# To construct phylogenetic tree 

```bash

#!/bin/bash

set -e

cd /NABIC/HOME/yedomon1/senthil/04_tree_construction/greaterthan500bp

#---Variable declaration

genes=above500bp.fasta

#---multiple sequence alignment

source activate mafft_env
mafft --maxiterate 1000 --localpair --thread 96 $genes > ${genes}.mafft
source deactivate mafft_env

#---alignment trimming
source activate trimal_env
trimal -automated1 -in ${genes}.mafft -out ${genes}.mafft.trimal
source deactivate trimal_env

#---Maximum Likehood tree construction with automatic model selection for each gene
source activate iqtree_env
iqtree -s ${genes}.mafft.trimal -nt AUTO
source deactivate iqtree_env

#--End

$ /usr/bin/time -o out.time.txt -v bash run.sh &> log &

```

