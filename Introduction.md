# Introduction
<p align="center">
  <img src="https://github.com/user-attachments/assets/0b65aa41-29cd-4f4e-9323-526eaec00aae" style="max-width: 100%; height: auto;">
</p>

Hello ! I am currently learning **Single Cell RNA Seq ANALYSIS**
As such, the first challenge I faced is finding and understanding the datasets and **How to load** them in R ( working on R ).
I am following an workshop tutorial in which is complex , so this repository is for documenting and practicing those elements that I learn from there. 

>[!TIP]
> Generally there are many ways to get the data sets and we can handle them in different ways.

1. 10x genomics

> [!NOTE]
> We will need 10x packages and also the seurat packages

We will first see how to read genomics data and load the seurat object for doing the analysis.
* Step 1
  * Get the data from [10xgenomics](https://cf.10xgenomics.com/samples/cell-exp/3.0.0/)
  * Load the data using `Read10X`
> [!WARNING]
> We need to install and load  `Seurat` package
```yaml annotate
library(Seurat)
data_dir <- "path_to_cellranger_output_folder/"  #directory
# What kind of object is this?
pbmc.data
seurat_obj <- Read10X(data.dir = data_dir) |> CreateSeuratObject()

```

Or, we can first read data using `Read10X` and assign it later if we keep our data in the working directory
```yaml annotate
### scRNA-Seq Analysis Workshop Module #1: Loading data into Seurat ###

# We will be using a public 10X Genomics scRNA-Seq dataset in PBMC cells
# You can read more 10X public datasets: https://www.10xgenomics.com/resources/datasets/
# Download the dataset if it is not already present
if (! file.exists("filtered_gene_bc_matrices/hg19/barcodes.tsv")) {
  download.file("https://cf.10xgenomics.com/samples/cell/pbmc3k/pbmc3k_filtered_gene_bc_matrices.tar.gz",
                destfile = "pbmc3k_filtered_gene_bc_matrices.tar.gz")
  untar("pbmc3k_filtered_gene_bc_matrices.tar.gz")
} 

## Following the Seurat Vignette: https://satijalab.org/seurat/articles/pbmc3k_tutorial.html ##
# Load the Seurat library
library(Seurat)

# Load the PBMC dataset
pbmc.data <- Read10X(data.dir = "filtered_gene_bc_matrices/hg19/")

# What kind of object is this?
pbmc.data

# Initialize the Seurat object with the raw (non-normalized data).
pbmc <- CreateSeuratObject(counts = pbmc.data)

# What kind of object is this?
pbmc

## That's all for today! ##
## Activity: Try finding a new single cell dataset and loading it into R ##
## Datasets can be found here: https://www.10xgenomics.com/resources/datasets/ ##
```
