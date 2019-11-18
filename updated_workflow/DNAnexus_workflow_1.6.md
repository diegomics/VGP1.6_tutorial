NEW VERSION -> work in progress <-
==================================
###### The idea is to use the old as a backbone, so I will start adding things to this: I thinks that this is the easyest way (TCV)
###### `code` and `parameters` and `buttons` and `folder/files structure`
**workflows** and **important names**

_Species ID_ and _other names_ and _**Species ID**_

"other names", "tabs"



# _fArcCen1_ Assembly Tutorial

This tutorial covers the assembly of the fish species [Flier Cyclid](https://vgp.github.io/genomeark/Archocentrus_centrarchus) (_Archocentrus centrarchus_) using the DNAnexus platform.
The overall assembly pipeline can be depicted in the following simplified chart:

![assembly chart 1.6](https://github.com/lunfardista/VGP1.6_tutorial/blob/master/updated_workflow/images/vgp_assembly_pipeline_1.6.png)


IMPORTANT: Remember that your questions are always welcome in training channel of Slack!

## Getting Started

When assigned an assembly, you will given a **Species ID** for your given genome (in this example _**fArcCen1**_) and a project will be shared with you containing the raw files for the genome which have been linked from the VGP AWS bucket.

The root folder of the project will have the _Species ID_ name (_fArcCen1_) and contain the following folders and files:

```
fArcCen1
└── genomic_data
    ├── 10x
    │   ├── fArcCen1_S1_L001_I1_001.fastq.gz
    │   ├── fArcCen1_S1_L001_R1_001.fastq.gz
    │   ├── fArcCen1_S1_L001_R2_001.fastq.gz
    │   ├── fArcCen1_S1_L002_I1_001.fastq.gz
    │   ├── fArcCen1_S1_L002_R1_001.fastq.gz
    │   ├── fArcCen1_S1_L002_R2_001.fastq.gz
    │   ├── fArcCen1_S1_L003_I1_001.fastq.gz
    │   ├── fArcCen1_S1_L003_R1_001.fastq.gz
    │   ├── fArcCen1_S1_L003_R2_001.fastq.gz
    │   ├── fArcCen1_S1_L004_I1_001.fastq.gz
    │   ├── fArcCen1_S1_L004_R1_001.fastq.gz
    │   └── fArcCen1_S1_L004_R2_001.fastq.gz
    ├── bionano
    │   ├── fArcCen1_Saphyr_DLE-1.cmap.gz
    │   ├── fArcCen1_Saphyr_DLE-1_1265239.bnx.gz
    │   └── fArcCen1_Saphyr_DLE-1_1265240.bnx.gz
    ├── pacbio
    │   ├── m54062_170721_074508.subreads.bam
    │   ├── m54062_170721_175442.subreads.bam
    │   ├── m54062_170722_040411.subreads.bam
    │   ├── m54062_170809_134833.subreads.bam
    │   ├── m54062_170809_234737.subreads.bam
    │   ├── m54142_170706_115228.subreads.bam
    │   ├── m54142_170707_122532.subreads.bam
    │   ├── m54142_170711_151050.subreads.bam
    │   ├── m54142_170712_212934.subreads.bam
    │   ├── m54142_170810_135956.subreads.bam
    │   ├── m54142_170810_235924.subreads.bam
    │   ├── m54144_170808_141859.subreads.bam
    │   ├── m54144_170809_001755.subreads.bam
    │   ├── m54144_170811_141157.subreads.bam
    │   ├── m54144_170812_001052.subreads.bam
    │   ├── m54144_170817_111904.subreads.bam
    │   ├── m54144_170817_211802.subreads.bam
    │   └── m54144_170818_072740.subreads.bam 
    └── phase (or arima)
        ├── fArcCen1_DDHiC_R1.fastq.gz
        ├── fArcCen1_DDHiC_R2.fastq.gz
        ├── fArcCen1_S3HiC_R1.fastq.gz
        └── fArcCen1_S3HiC_R2.fastq.gz


```

This includes 4 types of raw data:
1. 10X Genomics linked reads (`*.fastq.gz`)
2. Bionano optical maps (`*.cmap`)
3. Pacbio Sequel reads (`*.bam`)
4. HiC (provided by Arima or Phase Genomics) (`*.fastq.gz`)



To make sure the project is configured correctly, navigate to the "Settings" tab of the project. In addition to the project name (_**fArcCen1**_), the following fields should be configured as such:

```
Billed To: org-erich_lab
Region: AWS (US East)
Tags: Flier Cyclid
```


IMPORTANT: All work should be done in the project shared with you. Do **not** create a new project to work in.

## Falcon and Unzip Assembly

INSERT A BRIEF EXPLANATION ABOUT WHAT THIS STEP DOES AND WICH STAGES HAS <--- !!

Click the green button `+ Add Data` and search and select **VGP Tools** in the "Other Project" tab. Search and select the last version of the **vgp_falcon_and_unzip_assembly_workflow** and click the green button `Add Data`, after which a dialogue box will pop up with a progress bar indicating that the workflow has been copied to the current location of your working project.

In your working project, click the workflow to open it in _Run_ mode.

Before configuring the workflow, it is good practice to create an editable copy of the workflow in case anything is misconfigured or needs to be re-run. This can be done by selecting `Workflow Actions` and then selecting the `Save as template` action. This will take you to a copy of the workflow that can be modified. Workflows are automatically saved if any changes are made. Return to the `Run Analysis...` screen by clicking the `Start Analysis` button.

![Workflow Actions: Save as Template](https://raw.githubusercontent.com/VGP/vgp-assembly/master/tutorials/images/WorkflowSaveAsTemplate.png)

Look through the workflow to make sure all instances and inputs are configured correctly. Please check the following as they tend to be misconfigured:

. Under the `Unzip Track Reads` stage, the instance type should be set to `mem4_ssd1_x128`, unless something different is told to you in the training channel of Slack.

Once the workflow is configured, select the `BAM Files` input under the `BAM to FASTA` stage. This will pop up a dialogue window to select input files. Select the _PacBio Sequel Reads_ from the `pacbio` folder as input.

![BAM to FASTA input](https://raw.githubusercontent.com/VGP/vgp-assembly/master/tutorials/images/BAMtoFASTAinput.png)

Under the `Create Raw Reads Dazzler DB` stage, click the gear icon to open the parameters panel and fill in the "Estimated genome size" parameter with the given species' expected genome size. For `fArcCen1`, the estimated genome size is 0.99Gbp, so we fill in `0.99G`. The genome size can be obtained from the [Animal Genome Size Database](http://www.genomesize.com/) or if the species is no available there, can also be estimated by running **Jellyfish and GenomeScope** on the 10x Genomics reads (check at the end of this section about how to run the _Genomescope_ workflow).

![Create Raw Reads stage](https://raw.githubusercontent.com/VGP/vgp-assembly/master/tutorials/images/CreateRawReadsConfig.png)
![Configure genome size](https://raw.githubusercontent.com/VGP/vgp-assembly/master/tutorials/images/LengthCutoffConfig.png)

In addition to selecting parameters, it is useful to specify an output folder for the workflow. Under `Workflow Actions`, select `Set Output Folder`. Create a the follow folders with the name `assembly_vgp_standard_1.6` and then and select this as the output folder for the **vgp_falcon_and_unzip_assembly_workflow**. All of the output folders for the individual stages should already be configured. When the analysis is complete, there will be a total of 10 subfolders in your specified output folder, one for each stage of the workflow:

1. BAM to FASTA (bam_to_fasta)
2. FALCON stage 0 (stage_0)
3. FALCON stage 1 (stage_1)
4. FALCON stage 2 (stage_2)
5. FALCON stage 3 (stage_3)
6. FALCON Unzip stage 1 (unzip_stage_1)
7. FALCON Unzip stage 2 (unzip_stage_2)
8. FALCON Unzip stage 3 (unzip_stage_3)
9. FALCON Unzip stage 4 (unzip_stage_4)
10. FALCON Unzip stage 5 (unzip_stage_5)

All the stages of the workflow should now be in the "Runnable" state. Before running, make sure to save your workflow changes (including input specification) by selecting `Workflow Actions` and selecting `Update workflow with changes`. This will make it easier to modify and relaunch the workflow should any failures occur. Finally, click `Run as Analysis...` to launch the workflow.

![Remember to save your workflow configuration by clicking "Update Workflow with Changes"](https://raw.githubusercontent.com/VGP/vgp-assembly/master/tutorials/images/WorkflowUpdateWithChanges.png)
![Click the Run as Analysis button to launch the workflow.](https://raw.githubusercontent.com/VGP/vgp-assembly/master/tutorials/images/RunAsAnalysisGo.png)

Should any failures occur, the workflow can be restarted from the point of failure by navigating to the "Monitor" tab of the project and selecting the launched **vgp_falcon_and_unzip_assembly_workflow**. There you can select the `Rerun As Analysis` button. Be sure to wait while all inputs and links populate before making any changes to the analysis parameters.

The final output should look like this:
```
fArcCen1
├── assembly_vgp_standard_1.6
│   ├── bam_to_fasta
│   │   ├── m#####_######_######.subreads.fasta.gz
│   │   ├── m#####_######_######.subreads.fasta.gz
│   │   ├── m#####_######_######.subreads.fasta.gz
│   │   └── ...
│   ├── stage_0
│   │   ├── read_counts.csv
│   │   └── read_length_distribution.pdf
│   ├── stage_1
│   │   ├── genome_scope
│   │   ├── mer_counts.csv
│   │   ├── mer_counts.gs.log.png
│   │   ├── mer_counts.gs.png
│   │   ├── mer_counts.model.txt
│   │   ├── mer_counts.progress.txt
│   │   ├── mer_counts.summary.txt
│   │   ├── out.####.fasta.gz
│   │   ├── out.####.fasta.gz
│   │   ├── out.####.fasta.gz
│   │   ├── out.####.fasta.gz
│   │   ├── out.####.fasta.gz
│   │   ├── ...
│   │   ├── preads_rep.tar.gz
│   │   ├── preads_tan.tar.gz
│   │   ├── raw_reads.###.las
│   │   ├── raw_reads.###.las
│   │   ├── raw_reads.###.las
│   │   ├── raw_reads.###.las
│   │   ├── ...
│   │   ├── raw_reads_rep.tar.gz
│   │   ├── raw_reads_tan.tar.gz
│   │   │   └── read_counts.csv
│   │   └── read_length_distribution.pdf
│   ├── stage_2
│   │   ├── preads.###.las
│   │   ├── preads.###.las
│   │   ├── preads.###.las
│   │   └── ...
│   ├── stage_3
│   │   ├── a_ctg.fasta.gz
│   │   ├── a_ctg_tiling_path.gz
│   │   ├── asm.gfa.gz
│   │   ├── asm.gfa2.gz
│   │   ├── contig.gfa2.gz
│   │   ├── ctg_paths.gz
│   │   ├── p_ctg.fasta.gz
│   │   ├── p_ctg_tiling_path.gz
│   │   ├── preads4falcon.fasta.gz
│   │   ├── read_counts.csv
│   │   ├── read_length_distribution.pdf
│   │   ├── sg.gfa.gz
│   │   ├── sg.gfa2.gz
│   │   ├── sg_edges_list.gz
│   │   └── utg_data.gz
│   ├── unzip_stage_1
│   │   ├── ctg_list
│   │   ├── pread_ids.gz
│   │   ├── pread_to_contigs.gz
│   │   ├── rawread_ids.gz
│   │   ├── rawread_to_contigs.gz
│   │   ├── read_to_contig_map.gz
│   │   ├── reads_fastas_##.tar.gz
│   │   ├── reads_fastas_##.tar.gz
│   │   ├── reads_fastas_##.tar.gz
│   │   ├── reads_fastas_##.tar.gz
│   │   ├── ...
│   │   ├── ref_fastas_###.tar.gz
│   │   ├── ref_fastas_###.tar.gz
│   │   ├── ref_fastas_###.tar.gz
│   │   └── ...
│   ├── unzip_stage_2
│   │   ├── all_phased_reads.gz
│   │   ├── rid_to_phase.###.tar.gz
│   │   ├── rid_to_phase.###.tar.gz
│   │   ├── rid_to_phase.###.tar.gz
│   │   ├── rid_to_phase.###.tar.gz
│   │   ├── rid_to_phase.###.tar.gz
│   │   ├── rid_to_phase.###.tar.gz
│   │   └── ...
│   ├── unzip_stage_3
│   │   ├── all_h_ctg.fa.gz
│   │   ├── all_h_ctg_edges.gz
│   │   ├── all_h_ctg_ids.gz
│   │   ├── all_p_ctg.fa.gz
│   │   ├── all_p_ctg_edges.gz
│   │   ├── asm.gfa.gz
│   │   └── sg.gfa.gz
│   ├── unzip_stage_4
│   │   ├── contig_groups.json
│   │   ├── mappedread_###.tar.gz
│   │   ├── mappedread_###.tar.gz
│   │   ├── mappedread_###.tar.gz
│   │   ├── mappedread_###.tar.gz
│   │   └── ...
│   └── unzip_stage_5
│       ├── cns_h_ctg.fasta.gz
│       ├── cns_h_ctg.fastq.gz
│       ├── cns_p_ctg.fasta.gz
│       └── cns_p_ctg.fastq.gz
└── genomic_data

```

The `unzip_stage_5` folder contains the **Primary contigs** (`cns_p_ctg.fasta.gz`) and the **Alternate haplotigs**  (`cns_h_ctg.fasta.gz`), which will be used in the following steps of the assembly pipeline.

These two files must to be renamed using the convention of the VGP pipeline. To do this, first select the respective file and then click the pencil button that appears at the right to edit the name. In this example the name should be `fArcCen1_c1.fasta.gz` for the **Primary contigs** file, and `fArcCen1_c2.fasta.gz` for the **Alternate haplotigs** file.

Next, it is required that every intermediate assembly produced during the pipeline is placed in a specific folder. Navigate to the `assembly_vgp_standard_1.6` folder and click the green button `New Folder` to create a folder named `intermediates`. Move the `c1` and `c2` files to the `intermediates` folder by "drag and drop".

The final folder structure should look like this:
```
fArcCen1
├── assembly_vgp_standard_1.6
│   ├── bam_to_fasta
│   │   └── ...
│   ├── intermediates
│   │   ├── fArcCen1_c1.fasta.gz
│   │   └── fArcCen1_c2.fasta.gz
│   ├── stage_0
│   │   └── ...
.   .
^   ^
```

RUNNING **Jellyfish and GenomeScope**: To run correctly  this workflow, first the barcodes from the 10X reads have to be removed. In your working project, click the green button `+ Add Data` and search and select **VGP Tools** in the "Other Project" tab. Search and select the last version of the **proc10xg** applet. Click the applet to open it in _Run_ mode. For the input files, select all the `fastq.gz` in the `10x` folder. To specify an output folder for the workflow, under `Workflow Actions`, select `Set Output Folder`, navigate to the `assembly_vgp_standard_1.6` and create a new folder named `edited_reads`. Finally, click `Run as Analysis...` to launch the applet.
Once the task is finished, click the green button `Start Analysis` and search the **Jellyfish and GenomeScope** applet. For the input files, select all the `fastq.gz` in the `edited_reads` folder. Next, click the gear icon to open the parameters panel and set a k-mer length of `31`. To specify an output folder for the workflow, under `Workflow Actions`, select `Set Output Folder`, navigate to the `assembly_vgp_standard_1.6` and create a new folder named `genomescope`. Finally, click `Run as Analysis...` to launch the applet.



## Scaffolding

### 1. Purge Haplotigs

INSERT A BRIEF EXPLANATION ABOUT WHAT THIS STEP DOES AND WICH STAGES HAS <--- !!

In your working project, click the green button `+ Add Data` and search and select **VGP Tools** in the "Other Project" tab. Search and select the last version of the **Scaffold 1 purge_dups** workflow and click the green button `Add Data`, after which a dialogue box will pop up with a progress bar indicating that the workflow has been copied to the current location of your working project.

Click the workflow to open it in _Run_ mode and create an editable copy of it in case anything is misconfigured or needs to be re-run.
The inputs for the `purge_dups` stage are the **c1** file `fArcCen1_c1.fasta.gz` and the _PacBio Reads converted to fasta_ from the `bam_to_fasta` folder. Next, the input for the stage `concat c2+p2` is the **c2** file `fArcCen1_c2.fasta.gz`. 
Finally, under `Workflow Actions`, select `Set Output Folder`. Create a new folder with the name `Scaffolding` and select this as the output folder for the **Scaffold 1 purge_dups** workflow.

All stages of the workflow should now be in the "Runnable" state. Before running, make sure to save your workflow changes (including input specification) by selecting `Workflow Actions` and selecting `Update workflow with changes`. This will make it easier to modify and relaunch the workflow should any failures occur. Finally, click `Run as Analysis...` to launch the workflow.

Once finished, the final output should look like this:
```
fArcCen1
├── assembly_vgp_standard_1.6
│   ├── bam_to_fasta
│   │   └── ...
│   ├── intermediates
│   │   └── ...
│   ├── Scaffolding
│   │   ├── haplotig_purged
│   │   │   ├── fArcCen1_p2.fasta.gz
│   │   │   ├── fArcCen1_q2.fasta.gz
│   │   │   └── ...
│   │   ├── primary_purged
│   │   │   ├── fArcCen1_p1.fasta.gz
│   │   │   └── ...
│   │   ├── fArcCen1_c2p2.fasta.gz
│   │   ├── read_counts.csv
│   │   ├── read_counts.csv
│   │   ├── read_length_distribution.pdf
│   │   └── read_length_distribution.pdf
│   ├── stage_0
│   │   └── ...
.   .
^   ^
```

The **Curated primary** contigs should be contained in the file `fArcCen1_p1.fasta.gz`, and the **Alternate combined** haplotigs should be contained in the `fArcCen1_q2.fasta.gz` file.

At this point of the pipeline it is important to run several assembly metrics to check that all is going well so far. To do this, click the green button `+ Add Data` in your working project and search and select **VGP Tools** in the "Other Project" tab. Search and select the last version of the applets named `asm_stats` and `busco`, and the workflow named `Evaluation KAT Plot`.
To obtain the standard assembly statistics run the `asm_stats` applet using as input the respective assembly to be evaluated. In addition, click the gear icon and complete "Genome size (bp)" field with the size of the genome in base pairs and `fArcCen1` "species code" field. Create a new folder with the name `Stats` inside the `assembly_vgp_standard_1.6` folder and select it as the output folder. Check the 



Note: if the _Falcon and Unzip_ step was already run and the **c1** and **c2** are present in the `intermediates` folder but the `bam_to_fasta` folder is not present, you should run the applet **PacBio BAM to FASTA** which can be found in clicking the green button `Start Analysis`. The input of this applet are the _PacBio Sequel Reads_ from the `pacbio` folder and you should set up an output folder named `bam_to_fasta` inside the `assembly_vgp_standard_1.6` folder.


## 2. Scaff10x Workflow

The Scaff10x workflow performs two rounds of scaffolding with Scaff10x using the 10X Genomics raw reads. Copy the 
`Scaff10x 2 Rounds` workflow from the `VGP Tools` folder.

Select the file inputs for the first step of the workflow:
* assemble_genome_fastagz: This should be the _purged_ primary contigs from Purge Haplotigs (`curated.fasta.gz`)
* R1 reads: Under `genomic_data/10x`, all reads containing `_R1_*.fastq`
* R2 reads: Under `genomic_data/10x`, all reads containing `_R2_*.fastq`

Under the first round parameters, make sure the `is_raw` parameter is specified to `True`. Under both round 1 and round 
2 parameters you may also specify the output prefix for the output files if desired.

In addition, specify the `Output Folder` for the workflow to `scaffolding` as before. Launch the analysis.

![Configured Scaff10x workflow](https://raw.githubusercontent.com/VGP/vgp-assembly/master/tutorials/images/Scaff10XRunnable.png)

The final output of scaff10x should look like this:
```
scaffolding/scaff10x/
├── round1
│    ├── read-BC_1.fastq.gz
│    ├── read-BC_2.fastq.gz
│    └── scaffolds.fasta.gz
└── round2
     ├── read-BC_1.fastq.gz
     ├── read-BC_2.fastq.gz
     └── scaffolds.fasta.gz
```

The output under `round2/scaffolds.fasta.gz` corresponds to `fArcCen1_s1.fasta.gz` using the VGP naming convention.

## 3. Bionano Hybrid Scaffolding

In this step we will be using the Bionano assembled CMAP data together with the scaffold `fArcCen1_s1.fasta.gz` from 
step 2 to perform hybrid scaffolding on the primary haplotig.

Before copying the workflow, we need to first take a look at the Bionano input data:
```
genomic_data/bionano/
├── fArcCen1_Saphyr_DLE-1.cmap.gz
├── fArcCen1_Saphyr_DLE-1_1265239.bnx.gz
└── fArcCen1_Saphyr_DLE-1_1265240.bnx.gz
```

From the input data, we can see that there is a single `*.cmap.gz` file generated using the `DLE-1` enzyme. Therefore,
copy the `Step 3 Bionano Hybrid Scaffolding 1 Enzyme` workflow from VGP tools. In some cases you may see two `*.cmap.gz`
files in your input data corresponding to two enzymes used for the Bionano data, and therefore will need to use the 2 enzyme workflow.

For the inputs select as follows:
* CMAP input: `fArcCen1_Saphyr_DLE-1.cmap.gz` under `genomic_data/bionano/`
* FASTA input: `scaffolds.fasta.gz` under `scaffolding/scaff10x/round2`

As before, specify the workflow output folder to `scaffolding`. A `bionano` folder will be automatically created under that.

The Bionano tool is prone to hanging if the memory requirements are not met. Therefore, make sure it is running on a 
large memory instance, such as the `mem3_ssd1_x32` instance. The app is configured to aggressively time out if it does 
not complete in under 6 hours. If this happens, rerun the analysis on a larger memory instance.

Once the app completes, the output should look as follows:
```
scaffolding/bionano/
├── bn_pre_cut_projected_ngs_coord_annotations.bed
├── conflicts.txt
├── conflicts_cut_status.txt
├── conflicts_cut_status_CTTAAG.txt
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_BNGcontigs_HYBRID_SCAFFOLD.xmap
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_BNGcontigs_HYBRID_SCAFFOLD_q.cmap
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_BNGcontigs_HYBRID_SCAFFOLD_r.cmap
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_HYBRID_SCAFFOLD.cmap
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_HYBRID_SCAFFOLD_log.txt
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD.agp
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD.fasta
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD.gap
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD.xmap
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD_NCBI.fasta
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD_NOT_SCAFFOLDED.fasta
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD_q.cmap
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD_r.cmap
├── fArcCen1_Saphyr_DLE1_bppAdjust_cmap_scaffolds_fasta_NGScontigs_HYBRID_SCAFFOLD_trimHeadTailGap.coord
├── hybrid_scaffold_output.tar.gz
└── ngs_pre_cut_annotations.bed
```

As part of the Bionano hybrid scaffolding, you should also perform the following post-processing steps:
1. Concatenate `UNSCAFFOLDED` and `SCAFFOLD_FINAL_NCBI` outputs
2. Remove leading and trailing N's from scaffolded output.

To concatenate the two outputs, select the "Run Analysis" button in your project and select the "File Concatenator" app.

Supply the inputs `UNSCAFFOLDED` and `SCAFFOLD_FINAL_NCBI` to the app as well as the output name `fArcCen1_s2.fasta.gz`.

## Step 4. Salsa Scaffolding

Salsa scaffolding uses Hi-C data to scaffold the hybrid assembly from Bionano. Take a look at the HiC input data:
It will be located under the "genomic_data" folder with the name of the HiC provider who generated it, such as `phase`, `arima` or `dovetail`.
```
genomic_data/phase
├── fArcCen1_DDHiC_R1.fastq.gz
├── fArcCen1_DDHiC_R2.fastq.gz
├── fArcCen1_S3HiC_R1.fastq.gz
└── fArcCen1_S3HiC_R2.fastq.gz
```

In addition to the input files, you will need to know the restriction enzymes used to generate the data. For `fArcCen1`,
the sequences are `GATC`.

Copy the `Step 4 Salsa Scaffolding` workflow into your project. The workflow performs the following steps:

1. Align the HiC reads using the Arima mapping pipeline
2. Run Salsa2 on aligned reads and the s2.fasta.gz scaffold
3. Concatenate the output with the Haplotigs from FALCON Unzip

For configuring the inputs, select as follows:
* Under "Generate BWA Index Genome" stage, specify the scaffolded `fArcCen1_s2.fasta.gz` file for the `Genome` input.
* Under "Arima Mapping" stage, specify the paired end HiC for the `Forward Reads` (R1) and `Reverse Reads` (R2) inputs. 
* Under the "Salsa" stage, select the gear icon, and specify the HiC restriction enzyme (`GATC`) as the `Restriction enzyme bases` input.
* Under the "File Concatenator" stage, select the **Haplotig** output from FALCON Unzip Stage 5 
(`assembly_vgp_standard_1.6/unzip_stage_5/cns_h_ctg.fasta.gz`). 
* **Click and drag** the `Final Scaffold FASTA` output 
from Salsa to the File Concatenator `Files` input. You should see `1 File + 1 Link` listed as the input to the File Concatenator app.
* Click the gear icon next to the File Concatenator app to specify the output name: `fArcCen1_s4.fasta.gz`
* Configure `Scaffolding` as the output folder.

Here is what your configured workflow will look like:

![Configured Salsa workflow](https://raw.githubusercontent.com/VGP/vgp-assembly/master/tutorials/images/SalsaRunnable.png)

The final output should look like this:
```


```

## Step 5. Arrow Polishing

Arrow uses PacBio sequences (`subreads.bam`) to polish the scaffolds.

Inputs: 
- PacBio sequences (`subreads.bam`) 
- s4.fasta.gz

Copy the `Scaffold 5 Arrow Polish 2019-Sep-14` workflow into your project.The workflow performs the following steps:
1. Align the PacBio reads to the assembly using Minimap2.
2. Polish scaffolds using Arrow.

For configuring the inputs, select as follows:
* Add the PacBio data (`genomic_data/pacbio/*subreads.bam`, no `scraps.bam`!)
* Add s4.fasta.gz

After running the workflow:
- rename the output file in folder `polished_output/*_s4.arrow.fasta.gz` to `_t1.fasta.gz` and move it into the intermediates folder 
- generate assembly statistics with the tool `asm-stats` 
- export the data using the tool `DNAnexus to VGP S3 Exporter`


## Step 6. Freebayes Polishing

Freebayes use the concatenated output of purgedup and the output from salsato polish the ensamble

Input:
-s3 + q2 + mitotig: s4
- Out From SAlSA (I'm not sure about the name now TCV)

Copy the last version of "Scaffold 5 Arrow Polish"

The First input are the bam files from Pacbio (please don't include *.scraps.bam files)
As an opcional parameter you could include de *.pbi files from the Pacbio reads (in the same folder than Pacbio reads)
Then the S4 version of your ensamble and it's ready to submit!
As seen in the photo:

![magen](https://github.com/lunfardista/VGP1.6_tutorial/blob/master/updated_workflow/images/Screenshot%20from%202019-11-14%2014-59-10.png)



