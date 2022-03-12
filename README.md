
<!-- README.md is generated from README.Rmd. Please edit that file -->

# hgnc <img src='man/figures/logo.svg' align="right" height="139" />

<!-- badges: start -->
<!-- badges: end -->

The [HUGO Gene Nomenclature Committee
(HGNC)](https://www.genenames.org/) is a committee of the Human Genome
Organisation (HUGO) that sets the standards for human gene nomenclature.

The HGNC approves a unique and meaningful name for every known human
gene, based on a group of experts.

The goal of `{hgnc}` is to easily download and import HGNC gene data
into R.

## Installation

You can install the development version of `{hgnc}` like so:

``` r
# install.packages("remotes")
remotes::install_github("maialab/hgnc")
```

## Usage

To import the latest HGNC data set in tabular format directly into
memory as a tibble do as follows:

``` r
library(hgnc)

# Date of HGNC last update
last_update()
#> [1] "2022-03-10 02:03:59 UTC"

# Direct URL to the latest archive
(url <- latest_archive_url())
#> [1] "http://ftp.ebi.ac.uk/pub/databases/genenames/hgnc/tsv/hgnc_complete_set.txt"

# Import the data set in tidy tabular format
# NB: Multiple-value columns are kept as list-columns
hgnc_dataset <- import_hgnc_dataset_tsv(url)

dplyr::glimpse(hgnc_dataset)
#> Rows: 43,129
#> Columns: 55
#> $ hgnc_id                  <chr> "HGNC:5", "HGNC:37133", "HGNC:24086", "HGNC:7…
#> $ hgnc_id2                 <chr> "5", "37133", "24086", "7", "27057", "23336",…
#> $ symbol                   <chr> "A1BG", "A1BG-AS1", "A1CF", "A2M", "A2M-AS1",…
#> $ name                     <chr> "alpha-1-B glycoprotein", "A1BG antisense RNA…
#> $ locus_group              <chr> "protein-coding gene", "non-coding RNA", "pro…
#> $ locus_type               <chr> "gene with protein product", "RNA, long non-c…
#> $ status                   <chr> "Approved", "Approved", "Approved", "Approved…
#> $ location                 <chr> "19q13.43", "19q13.43", "10q11.23", "12p13.31…
#> $ location_sortable        <chr> "19q13.43", "19q13.43", "10q11.23", "12p13.31…
#> $ alias_symbol             <list> NA, "FLJ23569", <"ACF", "ASP", "ACF64", "ACF…
#> $ alias_name               <list> NA, NA, NA, NA, NA, NA, NA, NA, NA, <"iGb3 s…
#> $ prev_symbol              <list> NA, <"NCRNA00181", "A1BGAS", "A1BG-AS">, NA,…
#> $ prev_name                <list> NA, <"non-protein coding RNA 181", "A1BG ant…
#> $ gene_group               <list> "Immunoglobulin like domain containing", "An…
#> $ gene_group_id            <list> "594", "1987", "725", "1234", "1987", "1234"…
#> $ date_approved_reserved   <date> 1989-06-30, 2009-07-20, 2007-11-23, 1986-01-…
#> $ date_symbol_changed      <date> NA, 2010-11-25, NA, NA, NA, 2005-09-01, NA, …
#> $ date_name_changed        <date> NA, 2012-08-15, NA, NA, 2018-03-21, 2016-03-…
#> $ date_modified            <date> 2020-09-17, 2013-06-27, 2016-10-05, 2021-04-…
#> $ entrez_id                <int> 1, 503538, 29974, 2, 144571, 144568, 10087410…
#> $ ensembl_gene_id          <chr> "ENSG00000121410", "ENSG00000268895", "ENSG00…
#> $ vega_id                  <chr> "OTTHUMG00000183507", "OTTHUMG00000183508", "…
#> $ ucsc_id                  <chr> "uc002qsd.5", "uc002qse.3", "uc057tgv.1", "uc…
#> $ ena                      <list> NA, "BC040926", "AF271790", <"BX647329", "X6…
#> $ refseq_accession         <list> "NM_130786", "NR_015380", "NM_014576", "NM_0…
#> $ ccds_id                  <list> "CCDS12976", NA, <"CCDS7241", "CCDS73133", "…
#> $ uniprot_ids              <list> "P04217", NA, "Q9NQ94", "P01023", NA, "A8K2U…
#> $ pubmed_id                <list> "2591067", NA, <"11815617", "11072063">, <"2…
#> $ mgd_id                   <list> "MGI:2152878", NA, "MGI:1917115", "MGI:24491…
#> $ rgd_id                   <list> "RGD:69417", NA, "RGD:619834", "RGD:2004", N…
#> $ lsdb                     <chr> NA, NA, NA, "LRG_591|http://ftp.ebi.ac.uk/pub…
#> $ cosmic                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ omim_id                  <list> "138670", NA, "618199", "103950", NA, "61062…
#> $ mirbase                  <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ homeodb                  <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ snornabase               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ bioparadigms_slc         <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ orphanet                 <chr> NA, NA, NA, NA, NA, "410627", NA, NA, NA, NA,…
#> $ pseudogene.org           <chr> NA, NA, NA, NA, NA, NA, NA, NA, "PGOHUM000002…
#> $ horde_id                 <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ merops                   <chr> "I43.950", NA, NA, "I39.001", NA, "I39.007", …
#> $ imgt                     <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ iuphar                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ kznf_gene_catalog        <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ `mamit-trnadb`           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ cd                       <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ lncrnadb                 <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ enzyme_id                <list> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, "2.4…
#> $ intermediate_filament_db <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ rna_central_ids          <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ lncipedia                <chr> NA, "A1BG-AS1", NA, NA, "A2M-AS1", NA, "A2ML1…
#> $ gtrnadb                  <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ agr                      <chr> "HGNC:5", "HGNC:37133", "HGNC:24086", "HGNC:7…
#> $ mane_select              <list> <"ENST00000263100.8", "NM_130786.4">, NA, <"…
#> $ gencc                    <chr> NA, NA, NA, "HGNC:7", NA, "HGNC:23336", NA, N…
```

If you prefer to download the data set as a file to disk first, you can
use `download_archive()`.

The original data set does not contain the column `hgnc_id2`, which is
added as a convenience by `{hgnc}`; this is because although the HGNC
identifiers should formally contain the prefix `"HGNC:"`, it is often
found elsewhere that they are stripped of this prefix, so the column
`hgnc_id2` is also provided whose values only contain the integer part.
