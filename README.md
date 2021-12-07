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


# edit with online tools with the format of *mafft.trimal.treefile* 

[iTOL interactive tree of life](https://itol.embl.de/)

- step1: login: senthil83

- step2: upload tree file said above format.




[IQtree online platform to run Bootstrap value](http://iqtree.cibiv.univie.ac.at/)

- upload **.mafft file from IQtree** and mention mail id and submit job
- server upload and check working progress (Running!)
- after success the results and view the **full result** copy the newick format to notepad and save.

#Evolview online annotation#
[Evolview](https://www.evolgenius.info/evolview/#login)##
- login and upload the newick format and view circular tree format
- check the leaf and activate the bootstrap value to show in the tree
- choose the annotation (copy the code from the **help** and save as tablimited file for the labels annotation, mention the color for each group classification)
- 






