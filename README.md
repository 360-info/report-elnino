# El Niño

Visualises the working and impacts of El Niño, how El Niño affects global and regional temperatures, and how El Niño disrupts the Indian monsoon and crop production.

## Use + Remix rights

![[Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0)](https://mirrors.creativecommons.org/presskit/buttons/80x15/png/by.png)

These charts, as well as the analyses that underpin them, are available under a Creative Commons Attribution 4.0 licence. This includes commercial reuse and derivates.

<!-- Do any of the data sources fall under a different licence? If so, describe the licence and which parts of the data fall under it here! if most of it does, change the above and replace LICENCE.md too -->

Data in these charts and maps variously comes from:

- [WMO](https://public.wmo.int/en/media/press-release/wmo-update-prepare-el-ni%C3%B1o)
- [NASA Earth Observatory](https://earthobservatory.nasa.gov/features/ElNino/page3.php)
- [NASA Physical Sciences Laboratory](https://psl.noaa.gov/gcos_wgsp/Timeseries/Nino34/)
- [Berkeley Earth](https://berkeleyearth.org/data/)
- [PBS](https://www.pbs.org/newshour/show/somalia-in-need-of-humanitarian-aid-as-it-faces-worst-drought-in-decades)
- [Bertrand et al. (2020)](https://en.ird.fr/assessing-el-ninos-impact-fisheries-and-aquaculture-around-world)
- [Iese et al. (2021)](https://doi.org/10.1007/s10584-021-03112-1)
- [ICRISAT](http://data.icrisat.org)

**Please attribute 360info and the data sources when you use and remix these visualisations.**

## Reproduce the analysis

### 💨 Quickstart: use the dev container

This project comes with a ready-to-use [dev container](https://code.visualstudio.com/docs/remote/containers) that includes everything you need to reproduce the analysis (or do a similar one of your own!), including [R](https://r-project.org) and [Quarto](https://quarto.org).

1. [Launch this project in GitHub Codespaces](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=649496785)
2. If you have Docker installed, you can build and run the container locally:
  - Download or clone the project
  - Open it in [Visual Studio Code](https://code.visualstudio.com)
  - Run the **Remote-Containers: Reopen in Container** command

Once the container has launched (it might take a few minutes to set up the first time), you can run the analysis scripts with:

```sh
quarto render
```

Or look for the `.qmd` files to modify the analysis.

### Manual setup

To setup a development environment manually, 

You'll need to:
- [Download and install Quarto](https://quarto.org/docs/get-started)
- [Download the install R](https://www.r-project.org)
- Satisfy the R package dependencies. In R:
  * Install the [`renv`](https://rstudio.github.io/renv) package with `install.packages("renv")`,
  * Then run `renv::restore()` to install the R package dependencies.
  * (For problems satisfying R package dependencies, refer to [Quarto's documentation on virtual environments](https://quarto.org/docs/projects/virtual-environments.html).)

Now, render the `.qmd` files to the `/out` directory with:

```sh
quarto render
```

## Help

If you find any problems with our analysis or charts, please feel free to [create an issue](https://github.com/360-info/report-elnino/issues/new)!
