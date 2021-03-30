# Underscore Problem  

In some [`mathjaxr`](https://cran.r-project.org/web/packages/mathjaxr/mathjaxr.pdf) equations, the underscore symbol is converted into `\emph` when using [`devtools::document()`](https://www.rdocumentation.org/packages/devtools/versions/2.3.0/topics/document) to create the 'Rd' files from `roxygen2::roxygenize`.

This repository gives two examples of the problem: A, and B  

Workflow:  
1. `Sys.setenv(MATHJAXR_USECDN=TRUE)`    
2. `devtools::document()`   
3. `?Anotworking`
4. `?Aworking`
5. `?Bnotworking`
6. `?Bworking`

## Problem A: underscore as subscript       

Equation in the file Anotworking.R:   
`\hat{p}_c = \frac{1}{N} \sum_{i=1}^N B_{i,c}` 

How the equation is converted in `Anotworking.Rd`:   
`\hat{p}\emph{c = \frac{1}{N} \sum}{i=1}^N B_{i,c}`   

The problem seems to be with `{p}`.   

Equation in the file Aworking.R are converted correctly:
`p_{c} = \frac{1}{N} \sum_{i=1}^N B_{i,c}`

## Problem B: underscore as text   

Equation in the file `Bnotworking.R`:   
`w\_outlier_{i,c}B_{i,c}=1-\frac{d_{i,c}}{\lbrace {d_{j,c}} \rbrace}\lbrace {d_{j,c}}\rbrace`

How the equation is converted in `Bnotworking.Rd`:   
`w\\emph{outlier}{i,c}B_{i,c}=1-\frac{d_{i,c}}{\lbrace {d_{j,c}} \rbrace}\lbrace {d_{j,c}}\rbrace`

Similarly to before, the problem is at the start. When the underscore is replaced with a space, the equation in `Bworking.R` is converted correctly:  
`w\text{ }outlier_{i,c}B_{i,c}=1-\frac{d_{i,c}}{\lbrace {d_{j,c}`

### Session Information
R version 4.0.2 (2020-06-22)
Platform: x86_64-apple-darwin17.0 (64-bit)
Running under: macOS Catalina 10.15.

loaded via a namespace (and not attached):
 [1] Rcpp_1.0.5        mathjaxr_1.4-0    compiler_4.0.2    prettyunits_1.1.1
 [5] remotes_2.2.0     tools_4.0.2       testthat_2.3.2    digest_0.6.25    
 [9] packrat_0.5.0     pkgbuild_1.1.0    pkgload_1.1.0     memoise_1.1.0    
[13] lifecycle_0.2.0   rlang_0.4.10      cli_2.0.2         rstudioapi_0.11  
[17] commonmark_1.7    xfun_0.20         withr_2.4.1       stringr_1.4.0    
[21] roxygen2_7.1.1    knitr_1.28        xml2_1.3.2        desc_1.2.0       
[25] fs_1.4.2          devtools_2.3.2    rprojroot_1.3-2   glue_1.4.1       
[29] R6_2.4.1          processx_3.4.4    fansi_0.4.1       sessioninfo_1.1.1
[33] callr_3.5.1       purrr_0.3.4       magrittr_1.5      backports_1.1.8  
[37] ps_1.3.3          ellipsis_0.3.1    usethis_2.0.1     assertthat_0.2.1 
[41] tinytex_0.23      stringi_1.4.6     crayon_1.3.4   