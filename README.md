
<!-- README.md is generated from README.Rmd. Please edit that file -->
# ODER

<!-- badges: start -->
[![Lifecycle: experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://lifecycle.r-lib.org/articles/stages.html#experimental) [![BioC status](http://www.bioconductor.org/shields/build/release/bioc/ODER.svg)](https://bioconductor.org/checkResults/release/bioc-LATEST/ODER) [![R-CMD-check-bioc](https://github.com/eolagbaju/ODER/workflows/R-CMD-check-bioc/badge.svg)](https://github.com/eolagbaju/ODER/actions) [![Codecov test coverage](https://codecov.io/gh/eolagbaju/ODER/branch/master/graph/badge.svg)](https://codecov.io/gh/eolagbaju/ODER?branch=master) <!-- badges: end -->

The goal of `ODER` is **O**ptimising the **D**efinition of **E**xpressed **R**egions, which the package does by well defining the expressed regions from RNA-squencing experiments so that they can be confidently identified as pre-existing annotated exons or unannotated novel exons. ODER allows the user to vary two features -the MCC(Mean Coverage Cutoff) and MRG (Max Region Gap) - to generate various expressed regions and identifying the combination of MCC and MRG that most accurately defines the expressed region(s) by comparing it to a "gold standard" set of exons. This is done by calculating the exon delta (the absolute difference between the ER definition and the corresponding exon boundaries).

The optimally defined Expressed regions will be stored in the GenomicRanges GRanges class and ODER has several functions that will operate on these optimal ERs such as: 1. plotting the various exon deltas across MCCs and MRGs 2. annotating the ERs with junction data 3. refining annotated ERs using the junction data 4. generate a count matrix

## Installation instructions

Get the latest stable `R` release from [CRAN](http://cran.r-project.org/). Then install `ODER` using from [Bioconductor](http://bioconductor.org/) the following code:

``` r
if (!requireNamespace("BiocManager", quietly = TRUE)) {
    install.packages("BiocManager")
}

BiocManager::install("ODER")
```

And the development version from [GitHub](https://github.com/eolagbaju/ODER) with:

``` r
BiocManager::install("eolagbaju/ODER")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
# library("ODER")
# library("magrittr")
# # loading in RNA seq data to run ODER on
# gtex_metadata <- recount::all_metadata("gtex")
# gtex_metadata <- gtex_metadata %>%
#     as.data.frame() %>%
#     dplyr::filter(project == "SRP012682")
# url <- recount::download_study(
#     project = "SRP012682",
#     type = "samples",
#     download = FALSE
# )
# # .file_cache is an internal function to download a bigwig file from a link if the file has been downloaded recently, it will be retrieved from a cache
# bw_path <- ODER:::.file_cache(url[1])
# gtf_url <- "http://ftp.ensembl.org/pub/release-103/gtf/homo_sapiens/Homo_sapiens.GRCh38.103.chr.gtf.gz"
# gtf_path <- ODER:::.file_cache(gtf_url)
#
# # getting the optimally defined ERs by finding the combination of Mean Coverage Cut-off and Max Region Gap that gives the smallest exon delta
#
# # MCC - Mean Cutoff Coverage - this is the minimum read depth that a read needs to have to be considered expressed
# # MRG - Max Region Gap - this is the maximum number of base pairs between reads that fall below the MCC before you would not include it as part of the expressed region
# opt_ers <- ODER(
#     bw_paths = bw_path, auc_raw = gtex_metadata[["auc"]][1], # auc_example,
#     auc_target = 40e6 * 100, chrs = c("chr21", "chr22"),
#     genome = "hg38", mccs = c(2, 4, 6, 8, 10), mrgs = c(10, 20, 30),
#     gtf = gtf_path, ucsc_chr = TRUE, ignore.strand = TRUE,
#     exons_no_overlap = NULL, bw_chr = "chr"
# )
#
# # for stranded bigwig files:
#
# # bw_plus <- ODER:::.file_cache(url[58])
# # bw_minus <- ODER:::.file_cache(url[84])
# # opt_strand_ers <- ODER_strand(
# #     bw_pos = bw_plus, bw_neg = bw_minus,
# #     auc_raw_pos = gtex_metadata[["auc"]][58], auc_raw_neg = gtex_metadata[["auc"]][84],
# #     auc_tar_pos = 40e6 * 100, auc_tar_neg = 40e6 * 100, chrs = c("chr21", "chr22"),
# #     genome = "hg38", mccs = c(2, 4, 6, 8, 10), mrgs = c(10, 20, 30), gtf = gtf_path, ucsc_chr = TRUE, ignore.strand = FALSE,
# #     exons_no_overlap = NULL, bw_chr = "chr"
# # )
#
# opt_ers
# # opt_strand_ers
```

In that case, don't forget to commit and push the resulting figure files, so they display on GitHub!

## Citation

Below is the citation output from using `citation('ODER')` in R. Please run this yourself to check for any updates on how to cite **ODER**.

``` r
# print(citation('ODER'), bibtex = TRUE)
```

Please note that the `ODER` was only made possible thanks to many other R and bioinformatics software authors, which are cited either in the vignettes and/or the paper(s) describing this package.

## Code of Conduct

Please note that the `ODER` project is released with a [Contributor Code of Conduct](http://bioconductor.org/about/code-of-conduct/). By contributing to this project, you agree to abide by its terms.

## Development tools

-   Continuous code testing is possible thanks to [GitHub actions](https://www.tidyverse.org/blog/2020/04/usethis-1-6-0/) through *[usethis](https://CRAN.R-project.org/package=usethis)*, *[remotes](https://CRAN.R-project.org/package=remotes)*, and *[rcmdcheck](https://CRAN.R-project.org/package=rcmdcheck)* customized to use [Bioconductor's docker containers](https://www.bioconductor.org/help/docker/) and *[BiocCheck](https://bioconductor.org/packages/3.12/BiocCheck)*.
-   Code coverage assessment is possible thanks to [codecov](https://codecov.io/gh) and *[covr](https://CRAN.R-project.org/package=covr)*.
-   The [documentation website](http://eolagbaju.github.io/ODER) is automatically updated thanks to *[pkgdown](https://CRAN.R-project.org/package=pkgdown)*.
-   The code is styled automatically thanks to *[styler](https://CRAN.R-project.org/package=styler)*.
-   The documentation is formatted thanks to *[devtools](https://CRAN.R-project.org/package=devtools)* and *[roxygen2](https://CRAN.R-project.org/package=roxygen2)*.

For more details, check the `dev` directory.

This package was developed using *[biocthis](https://bioconductor.org/packages/3.12/biocthis)*.
