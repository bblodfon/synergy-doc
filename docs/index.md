---
title: "On Synergy"
author: "John Zobolas"
date: "Last updated: 15 December, 2020"
description: "A book about synergy models"
url: 'https\://bblodfon.github.io/synergy-doc/'
github-repo: "bblodfon/synergy-doc"
bibliography: ["references.bib", "packages.bib"]
link-citations: true
site: bookdown::bookdown_site
---



# Preface {-}

## Updates {-}

- **September 2020**: Almost a year with no writing and for a good reason! I won't be doing anything related to synergy in my PhD, expect from [this analysis](https://druglogics.github.io/sintef-obs-synergies/).
This means this is going to be left as it is for now, the full notes are still available in the [Word doc](https://github.com/bblodfon/synergy-doc/blob/main/notes_synergy.docx) if you wanna check them out.
Sorry :(
- **Summer 2020**: Read an amazing review article about synergy models [@Meyer2020], not so much from the mathematical perspective, but much more broad and interesting!
It introduced to several other mathematical formulas which I wasn't aware of when I wrote the notes, so more reading, more writing!
- **November 2019**: I thought of making this as a bookdown [@R-bookdown] document since it would be nicer to have it in that format for online reading, boost it's *accessibility* to the scientific community and add a means to collaborate (via Travis + bookdown's Edit button).
It's gonna take some time to write it down though from the [Word document](https://github.com/bblodfon/synergy-doc/blob/main/notes_synergy.docx)
- **Summer 2018**: I read a bunch of papers related to synergy quantification and models that describe it and wrote a [Word document](https://github.com/bblodfon/synergy-doc/blob/main/notes_synergy.docx) with my notes.
My motivation is to understand the mathematics behind the different models that are used to computationally assess synergy, antagonism or non-interaction between drugs that are tested in high-throughput screens, and compare/assess their weak and strong points.

## What is this about? {-}

A collection of **personal notes** regarding mathematical models that describe synergy.
Like a math textbook so to speak.
So, **not a review paper** or a book for that matter, just nicely structured, incomplete, personal notes.

Note that I have copied statements used in the papers exactly as they were written (so full plagiarism).
They wrote it, they said it, it is what it is!

If these notes help you, then amazing!
If you want to contribute, you are most welcome, do a PR please!

And remember, as one of my supervisors once said:

> What is a mountain, what is a synergy?

...and after a while, we concluded at:

> The mountain *is* the synergy!

## Structure {-}

TODO

## Software Information {-}

The most important thing is to install is the bookdown package [@R-bookdown]. 


```r
xfun::session_info()
```

```
## R version 3.6.3 (2020-02-29)
## Platform: x86_64-pc-linux-gnu (64-bit)
## Running under: Ubuntu 20.04.1 LTS
## 
## Locale:
##   LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
##   LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
##   LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
##   LC_PAPER=en_US.UTF-8       LC_NAME=C                 
##   LC_ADDRESS=C               LC_TELEPHONE=C            
##   LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       
## 
## Package version:
##   base64enc_0.1.3 bookdown_0.21   compiler_3.6.3  digest_0.6.27  
##   evaluate_0.14   glue_1.4.2      graphics_3.6.3  grDevices_3.6.3
##   highr_0.8       htmltools_0.5.0 jsonlite_1.7.2  knitr_1.30     
##   magrittr_2.0.1  markdown_1.1    methods_3.6.3   mime_0.9       
##   rlang_0.4.9     rmarkdown_2.6   stats_3.6.3     stringi_1.5.3  
##   stringr_1.4.0   tinytex_0.28    tools_3.6.3     utils_3.6.3    
##   xfun_0.19       yaml_2.2.1
```
