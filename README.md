# anushkaseth.github.io

This repository contains the source for a Quarto personal website and blog. Its
posts include Python notebooks, R analyses, and an analysis that combines R and
Python.

## Prerequisites

Install these tools before following the commands below:

- Git.
- Quarto 1.10.18 (the version used for these instructions): [install Quarto](https://quarto.org/docs/get-started/).
- R 4.6.1, as recorded in `renv.lock`: [install R](https://cran.r-project.org/).
- [uv](https://docs.astral.sh/uv/getting-started/installation/). The repository does not pin a uv version; install the current stable release.

The repository pins Python 3.14 in `.python-version`; `uv` will use it when
creating the environment. The R project library is bootstrapped by `renv` when
you run the restore command below. Open a fresh terminal after installing the
tools and confirm `git`, `quarto`, `Rscript`, and `uv` are available on `PATH`.

## Clone, set up, and render

Run the following commands in order. The shell commands work in macOS Terminal
and Windows PowerShell unless marked otherwise. Run every `cd` and setup command
from the terminal; the R restore command is run from the repository root.

1. Clone and enter the repository:

	```sh
	git clone https://github.com/AnushkaSeth/anushkaseth.github.io.git
	cd anushkaseth.github.io
	```

2. Restore the R packages from `renv.lock`. Run this in the shell at the
	repository root; `.Rprofile` bootstraps `renv` if needed:

	```sh
	Rscript -e "renv::restore()"
	```

	Alternatively, start R from the repository root and run `renv::restore()`
	at the R prompt.

3. Install the locked Python dependencies and create `.venv`:

	```sh
	uv sync --locked
	```

4. Render the complete site, pointing Quarto and `reticulate` to the project's
	Python environment. On macOS, run:

	```sh
	export QUARTO_PYTHON="$PWD/.venv/bin/python"
	export RETICULATE_PYTHON="$PWD/.venv/bin/python"
	quarto render
	```

	On Windows PowerShell, run instead:

	```powershell
	$env:QUARTO_PYTHON = "$PWD\.venv\Scripts\python.exe"
	$env:RETICULATE_PYTHON = "$PWD\.venv\Scripts\python.exe"
	quarto render
	```

## Output and data

The built website is written to `docs/`. To view it locally, run `quarto
preview` from the repository root; Quarto serves the site and opens it in a
browser. You can also open `docs/index.html` directly.

The computational posts use the Palmer Penguins data, originally collected by
Palmer Station Antarctica LTER, through the installed `palmerpenguins` R and
Python packages. The build does not separately download the dataset. An internet
connection is needed during setup to install Quarto if not already installed
and to restore R and Python packages; rendering itself does not fetch the data.