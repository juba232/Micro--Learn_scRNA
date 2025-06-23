# Introduction
<p align="center">
  <img src="https://github.com/user-attachments/assets/0b65aa41-29cd-4f4e-9323-526eaec00aae" style="max-width: 75%; height: auto;">
</p>

Hello ! I am currently learning **Single Cell RNA Seq ANALYSIS**
As such, the first challenge I faced is finding and understanding the datasets and **How to load** them in R ( working on R ).
I am following an workshop tutorial in which is complex , so this repository is for documenting and practicing those elements that I learn from there. 

>[!TIP]
> Generally there are many ways to get the data sets and we can handle them in different ways.

1. 10x genomic

We will first see how to read genomics data and load the seurat object for doing the analysis.
* Step 1
  * Get the data from [10xgenomics](https://10xgenomics.com)
  * Load the data using `Read10X`
> [!WARNING]
> What file type we will mostly get from 10x genomics? Well most files are zipped file and has more or less three files
 * barcode.tsv
 * genes.tsv
 * matrix.mtx

What those files mean ? :: *barcode* and *genes* are in `tsv` file formnat which is **text** files, `genes` are the row names meaning the actual sequence and the `barcode` is **Cell** names and the *matrix.mtx* is `matrix` file of the gene counts. if we combine these three files we will get typical `RNA` sequencing data having row names provided by gene.tsv file and column names provided by barcode meaning which cell the RNA string belongs. 

```yaml annotate
 #Download the dataset if it is not already present
if (! file.exists("filtered_gene_bc_matrices/hg19/barcodes.tsv")) {
  download.file("https://cf.10xgenomics.com/samples/cell/pbmc3k/pbmc3k_filtered_gene_bc_matrices.tar.gz",
                destfile = "pbmc3k_filtered_gene_bc_matrices.tar.gz")
  untar("pbmc3k_filtered_gene_bc_matrices.tar.gz")
} 
```
<div align="center">
<table>
<tbody>
<td align="center">
<img width="2000" height="0"><br>
<sub>SO WHAT DOES IT DO?</sub><br>
<img width="200" height="0">
</td>
</tbody>
</table>
</div>

WHat it does is , you give a link of a dataset that 10Xgenomics host and then it will automatically download the `.tar` file if that is not exist in the directory
and then it will `unter` it for being able to read it using `Read10X` command in R. lets see how
```yaml annote
#reading the data from the working directory
library(Seurat)

# Load the PBMC dataset
pbmc.data <- Read10X(data.dir = "filtered_gene_bc_matrices/hg19/")
```
notice here `filtered_gene_bc_matrices/hg19/` is chosen for data directory, so when we **untar** the dowloaded file we get a folder named **filtered_gene_bc_matrices** and in this folder we get another folder named **hg19** where we have those three files, so `Read10X` will automatically detect them and if we assign it as an `.data` object , we can then make a seurat object out of it. like this 
```yaml annote
#creating seurat object
pbmc <- CreateSeuratObject(counts - pbmc.data)
# What kind of object is this?
pbmc
```

<div align="center">
<table>
<tbody>
<td align="center">
<img width="2000" height="0"><br>
<sub>SO How Can We Get Links?</sub><br>
<img width="200" height="0">
</td>
</tbody>
</table>
</div>

Finding datasets in 10X genomic is quite easy.. lets take a look when we visit this website and naviget to `Resources/Dataset`



<p align="center">
  <img src="https://github.com/user-attachments/assets/57646eb0-33cc-4e9b-97d0-07cfae901103" style="max-width: 75%; height: auto;">
</p>


lets chose any dataset from here , say this dataset `2.5k Wistar Rat PBMCs Singleplex Sample` . all we gotta do is to click **Output and supplemental files**

<p align="center">
  <img src="https://github.com/user-attachments/assets/f0a9c9e1-3641-4a9c-b8cb-65d6433d39c0" style="max-width: 75%; height: auto;">
</p>

and form there we nedd to that says `HD5` .. this file comes with those three files we talked before. 
<p align="center">
  <img src="https://github.com/user-attachments/assets/96747120-ee2d-43f5-927c-216ac0df0f44" style="max-width: 75%; height: auto;">
</p>

from the top we can select `Batch Download` for the links we need to put in the code that we have shown before. see here,

<p align="center">
  <img src="https://github.com/user-attachments/assets/12e53273-24a9-4b67-aa43-962c5d16e332" style="max-width: 75%; height: auto;">
</p>

What we are mostly looking for files that end wit `.tar.gz` as this type of files are the gene expression dataset that we need to work on
