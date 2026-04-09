# Data preprocessing for GOTTA: SMA mouse brain

This repository contains the R Markdown workflow used to preprocess SMA mouse brain spatial multimodal data into `Seurat` objects that can be consumed by [GOTTA](https://github.com/WuJianHITSZ/gotta) for downstream geometric and multimodal analysis.

The project is focused on preparing aligned MSI and Visium data, integrating them into multimodal `Seurat` objects, adding curated metadata, and exporting a lightweight quick-start example object for the GOTTA package.

The workflow and repository presentation were prepared with the structure of the original SMA project in mind, and the source data lineage comes from the public [marcovito/sma](https://github.com/marcovito/sma) repository.

## Repository purpose

This repository documents and preserves the preprocessing steps used for the SMA mouse brain branch of the GOTTA workflow:

- align MSI and RNA spatial coordinates into a shared coordinate system
- compute cross-modal nearest-neighbor mappings
- build multimodal `Seurat` objects with RNA and MSI assays
- run a baseline joint analysis
- attach metadata exported from Loupe Browser
- create a trimmed example object for GOTTA quick-start demonstrations

## Project layout

- `1_reproduce_aligned_coordinates.Rmd`: reconstructs aligned coordinates from merged spatial objects
- `2_filter_RNA_spots_via_KNN.Rmd`: filters RNA spots using spatial nearest-neighbor constraints
- `3_integration_via_KNN.Rmd`: builds RNA+MSI multimodal `Seurat` objects
- `4_joint_analysis.Rmd`: performs baseline single-modality and multimodal analysis
- `5_add_metadata_1.Rmd`: adds lesion, region, and `RegionLoupe` metadata
- `6_make_quick_start_toy_object.Rmd`: exports a full example object and a GOTTA quick-start toy object
- `MSI_SRT_mPD_LL.Rproj`: optional RStudio project file

## Data provenance

The underlying SMA data originate from the public SMA project:

- upstream repository: [marcovito/sma](https://github.com/marcovito/sma)
- article context: *Spatial Multimodal Analysis of Transcriptomes and Metabolomes in Tissues*

This repository does not bundle the original raw datasets. Instead, it assumes that processed intermediate objects already exist locally and can be loaded from the paths referenced in the scripts.

## Expected inputs

The scripts currently reflect the author's local working setup and expect precomputed `.rds` objects to be available in locations such as:

- `~/Documents/gotta/data/`
- `~/Documents/gotta/result/`
- `C:/Users/jian/Documents/R/result/`

In particular, the final quick-start export step expects `se.multi.list` to be available in `C:/Users/jian/Documents/R/result/se.multi.list` or one of the fallback paths defined in `6_make_quick_start_toy_object.Rmd`.

## How to run

Run the numbered R Markdown scripts in order:

1. `1_reproduce_aligned_coordinates.Rmd`
2. `2_filter_RNA_spots_via_KNN.Rmd`
3. `3_integration_via_KNN.Rmd`
4. `4_joint_analysis.Rmd`
5. `5_add_metadata_1.Rmd`
6. `6_make_quick_start_toy_object.Rmd`

These scripts are designed to be executed interactively in RStudio or chunk-by-chunk in an R session after the required input objects are available.

## Dependencies

The workflow uses R packages that are loaded directly inside the scripts, including:

- `STutility`
- `SeuratObject`
- `Matrix`
- `dplyr`
- `dbscan`

Additional packages may be required depending on which parts of the workflow you execute.

## Outputs

Representative outputs created by this workflow include:

- aligned coordinate tables
- nearest-neighbor mapping tables
- multimodal `Seurat` object lists
- metadata-augmented `Seurat` objects
- a trimmed quick-start object copied into the GOTTA package `inst/extdata` directory

## Notes

- Path handling in the current scripts is intentionally close to the original working notebooks and may need small edits on another machine.
- If any script text mentions mouse heart, interpret this repository as the mouse brain preprocessing branch for GOTTA.
