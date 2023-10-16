(Insert GitHub Actions/codecov status badges here)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

# README

## Prerequisites
Create a new repository for your module on GitHub with no files.

Create a new Python 3.10 (install it beforehand) virtual environment using `venv` and switch to it.

```
python3.10 -u -m venv ~/venv-hkpythonoctwebinar ;
```

```
source ~/venv-hkpythonoctwebinar/bin/activate && pip install --upgrade pip ;
```

## Create a new module

Running in the above venv:

```
(venv-hkpythonoctwebinar) $ git clone git@github.com:nth10sd/hkpythonoctwebinar.git

(venv-hkpythonoctwebinar) $ git clone REPLACEME
                            ^^^^^^^^^

(venv-hkpythonoctwebinar) $ cd REPLACEME
                     ^^^^^^^^^

(venv-hkpythonoctwebinar) $ cp -r ../hkpythonoctwebinar/* ../hkpythonoctwebinar/.gitignore ../hkpythonoctwebinar/.vulture_allowlist ../hkpythonoctwebinar/.github . && rm -rf build/ *.egg*-info/

(venv-hkpythonoctwebinar) $ mv hkpythonoctwebinar/ REPLACEME
                                ^^^^^^^^^

(venv-hkpythonoctwebinar) $ find . ! \( -path ./.git -prune \) -type f | xargs sed -i 's/hkpythonoctwebinar/REPLACEME/g'
                                                                                         ^^^^^^^^^
```

Install your module by running:

```
(venv-hkpythonoctwebinar) $ pip install --upgrade -r requirements.txt && pip install --upgrade -e .
```

Run your new module using:

```
(venv-hkpythonoctwebinar) $ python -u -m REPLACEME
                               ^^^^^^^^^
```

Delete the CodeQL steps in the GitHub Actions `.yml` workflow settings file if they are not required.

## Run tools on your package

(All commands here must be run within the `venv`, in the main repository directory - not any subfolders)

For linters only:
```
for TOOL in ruff mypy pylint ; do "$TOOL" $(python -c "from pathlib import Path; exec('try: import tomllib\nexcept ImportError: import tomli as tomllib\nwith Path(\"pyproject.toml\").open(mode=\"rb\") as fp:\n cfg = tomllib.load(fp)\n print(f\'{cfg[\"project\"][\"name\"]}/{\" tests/\" if Path(\"tests/\").is_dir() else \"\"}\')')") ; done;
```

For comprehensive tests and all linters:
```
python -u -m pytest --black --cov --mypy --pylint --ruff
```

For comprehensive tests and all linters **except** slow tests:
```
python -u -m pytest --black --cov --mypy --pylint --ruff -m "not slow"
```

## Documentation generation via Sphinx

* Change into `docs/` folder: `cd docs/`
* Run generation command - you **must** first be in the `docs/` directory: `./gen-sphinx-html.sh`
* Your generated HTML files are now in `docs/build/html/` directory
* Open `index.html` to start
