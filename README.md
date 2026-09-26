# anushkaseth.github.io

## Render the site locally

These steps clone the repository, install the R and Python dependencies used by
the posts, and render the complete Quarto website. The first setup downloads
packages from CRAN and PyPI, so an internet connection is required.

### Install the prerequisites

Install Git, [Quarto](https://quarto.org/docs/get-started/), [R 4.6.1](https://cran.r-project.org/)
(the version recorded in `renv.lock`), and [uv](https://docs.astral.sh/uv/getting-started/installation/).
The committed `.python-version` selects Python 3.14. Make sure `git`, `quarto`,
`Rscript`, and `uv` are available in a new terminal.

### Clone the repository

Run these commands in Terminal on macOS or PowerShell on Windows:

```sh
git clone https://github.com/AnushkaSeth/anushkaseth.github.io.git
cd anushkaseth.github.io
```

### Restore R packages

From the repository directory, run:

```sh
Rscript -e "renv::restore()"
```

This restores the R packages recorded in `renv.lock`, including packages used
by the R posts and the R-Python post.

### Set up Python

From the repository directory, run this command in Terminal on macOS or
PowerShell on Windows:

```sh
uv sync --locked
```

This creates `.venv` and installs the exact dependencies from `uv.lock`.

### Render all posts and pages

Run the commands below from the repository directory. They point both Quarto's
Jupyter engine and R's `reticulate` package to the local Python environment,
which is needed by the notebook and the post that combines R and Python.

On macOS:

```sh
export QUARTO_PYTHON="$PWD/.venv/bin/python"
export RETICULATE_PYTHON="$PWD/.venv/bin/python"
quarto render
```

On Windows PowerShell:

```powershell
$env:QUARTO_PYTHON = "$PWD\.venv\Scripts\python.exe"
$env:RETICULATE_PYTHON = "$PWD\.venv\Scripts\python.exe"
quarto render
```

Quarto renders the website and its posts into `docs/`. To preview the rendered
site locally, open `docs/index.html` in a browser.