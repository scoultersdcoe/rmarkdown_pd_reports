# rmarkdown-factsheets

## Overview

This repository contains tools and templates for creating the San Diego County Office of Education's, PDF reports in [R Markdown](https://rmarkdown.rstudio.com/). These resorts are closed from the Urban Institute's information on factsheets , read [Iterated fact sheets with R Markdown](https://medium.com/@urban_institute/iterated-fact-sheets-with-r-markdown-d685eb4eafce) and [Iterated PDFs with R Markdown](https://medium.com/@urban_institute/iterated-pdfs-with-r-markdown-144e2a6d6a1a).

## Getting started

### Lato font

SDCOE uses the font [Segoe UI](https://fonts.google.com/specimen/SegoeUI). Go to `Control Panel` > `Appearance and Personalization` > `Fonts` to see if Segoe UI is installed on your computer. 

Fonts are embedded in the PDFs with the [Cairo graphics library](https://www.cairographics.org/). Cairo is installed when R is installed. On Macs, Cairo won't work unless [XQuartz](https://www.xquartz.org/) is installed. 

### LaTeX distribution

Creating PDFs with R Markdown requires a [LaTeX](https://www.latex-project.org/about/) distribution. In the past, this too often meant installing and maintaining the large and clunky MiKTeX. Fortunately, Yihui Xie created TinTeX, a custom LaTeX distribution based on TeX Live that is lightweight and can be managed in R.

Submit the following code in R to install TinyTex ([full instructions here](https://yihui.name/tinytex/)):

```
install.packages(c("tinytex", "rmarkdown"))
tinytex::install_tinytex()
```
**Note:** If you installed MiKTeX in the past, uninstall it before installing TinyTex. 

### Fork or download this repository

Fork this repository or download the contents of this repository to get access to the template. Using [R Projects](https://ui-research.github.io/r-at-urban/intro-to-r.html#projects) with the template is highly recommended and an R Project is included in the repository.  

## Use

`preamble.tex` and `template.Rmd` contain settings and code to put R Markdown PDFs into SDCOE's report style. Many of the changes are automated. 

### Macros

Some of the changes require using custom LaTeX macros:

* `\contactinfo{}` Adds SDCOE's contact information to the end of the page. 
* `\sdcoelogo{}` Add SDCOE's logo to the top left of the page
* `\sdcoetitle{}` Adds formatted title. **Argument:** title text
* `\sdcoesubtitle{}` Adds formatted subtitle. **Argument:** text subtitle
* `\sdcoeauthors{}` Adds formatted byline. **Argument:** byline text
* `\sdcoesubhead{}` Adds formatted subhead. **Argument:** subhead text
* `\sdcoefigurenumber{}` Adds formatted figure label. **Argument:** figure number
* `\sdcoefiguretitle{}` Adds formatted figure title. **Argument:** figure title
* `\sdcoesource{}` Adds formatted figure source. **Argument:** figure source
* `\sdcoenote{}` Adds formatted figure note. **Argument:**  figure note
* `\sdcoeboilerplate{}{}{}` Adds SDCOE's boilerplate to end of current page. **Arguments:** funder name, month, year. **Note:** The boilerplate is in an absolute position, not a relative position. 
* `\sdcoetablenumber{}` Adds formatted table number. **Argument:** table number
* `\sdcoetabletitle{}` Adds a formatted table title. **Argument:** table title text
* `\sdcoetablesubtitle{}` Adds formatted table subtitle. **Argument:** table subtitle text


### Environments

Some of the changes require using custom LaTeX environments:

* `\sdcoebullets{}` Creates an environment for styled bullets. Use:

```
\begin{sdcoebullets}
  \item bullet text
  \item bullet text
  \item bullet text
\end{sdcoebullets}
```

* `\sdcoeenumerate{}` Creates an environment for styled bullets. Use:

```
\begin{sdcoeenumerate}
  \item list text
  \item list text
  \item list text
\end{sdcoeenumerate}
```

### Data visualizations

Styled data visualizations can be created with [urbnthemes](https://github.com/UI-Research/urbnthemes). Install the package and include the following at the top of the `.Rmd` file:

```
library(tidyverse)
library(urbnthemes)

set_urbn_defaults(style = "print")
```

## General guidelines

* No text smaller than 9 point.
* All headings and body text (including bullets, table text, etc.) should be flush left.
* First-level headings should be the second-most-prominent text on the page and should include a visual break (i.e., blank space). 12 pt Segoe UI, bold, 12 points of space before the paragraph.
* Titles, subtitles, and author names should be centered at the top of page one.
* The title should be the most prominent text on page 1. Titles should be 15 pt Segoe UI, bold, black.
* Subtitles should be 12 pt Segoe UI, regular, Urban blue.
* Author name(s) should appear on page 1 under the title (and subtitle, if applicable). Author name(s) should be 11 pt Segoe UI, italic, black, 12 points of space after the paragraph.
* Make heavy use of the [Urban Institute Data Visualization Style Guide](http://urbaninstitute.github.io/graphics-styleguide/)
* Hyperlinks should be included using `\href{}{}`

## Iteration

The template (for example, simple-factsheet.Rmd) is iterated with the `iterate.R` script. 

`iterate.R` takes an index, creates a data frame with outfile names and parameters, and iterates the template across each row of the data frame. 

## Contributors

### Creator

* Aaron Williams

### Contributors

