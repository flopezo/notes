# Using the R package `vitae`

## Installing `vitae`

```
# Install the release version from CRAN

install.packages('vitae')
```

`viate` requires `LaTeX` to be installed. 

I had `MacTex` installed (`BasicTeX`) already. However, the `BasicTeX` distribution lacks some of the packages needed to knit to `awesomecv`. I had to install missing packages using the `Tex Live Utility` (found in Applications on macOS).


The `tinytex` package makes it easy to setup `LaTeX` within R:

```
install.packages('tinytex')
tinytex::install_tinytex()
```

## Getting started

From the [`vitae` documentation](https://github.com/mitchelloharawild/vitae):
```
The vitae package currently supports 5 popular CV templates, and adding more is a relatively simple process (details in the creating vitae templates vignette).

Creating a new CV with vitae can be done using the RStudio R Markdown template selector.
```

The documentation also includes examples. I followed one of these examples and needed to install additional packages, such as `fontawesome`:

```
load_cran_pkgs <- function(pkg) {
  new_pkg <- pkg[!(pkg %in% installed.packages()[, "Package"])]
  if (length(new_pkg)) {
    install.packages(new_pkg, dependencies = TRUE)
  }
  sapply(pkg, require, character.only = TRUE)
}

cran_pkgs <- c(
  "tidyverse", "ggrepel", "emojifont", "kableExtra", "huxtable",
  "gridExtra", "stplanr", "vitae", "rorcid"
  # "tinytex"
)
load_cran_pkgs(cran_pkgs)
# tinytex::install_tinytex()

devtools::install_github("rstudio/fontawesome")
library(fontawesome)
```

After installing `vitae` and other packages, knit the file in `RStudio` using the `knit to awesomecv` option. The main sections of the CV will have icons next to the headings. The full list of `FontAwesome` icons can be found [here](http://mirrors.ibiblio.org/CTAN/fonts/fontawesome5/doc/fontawesome5.pdf); include icons like so: `\faIcon{file} Publications`.

## Edit the `awesome-cv` template

The file `"awesome-cv.cls"` contains all the configuration details for fonts, spacing, etc. I changed the  `\fontsize` elements and added `/Library/Fonts/` to `\fontdir`, enabling the use of other installed fonts such as `Open Sans`. I also copied, pasted, and renamed some font files to match the filenames needed for knitting (e.g., I created a copy of `OpenSans-Semibold.ttf`, which I renamed to `OpenSans-Medium.ttf`). Search for the `\newfontfamily` element to find the default font type (`Roboto`).
