# uv
modern, extremely fast python package and project manager
written in rust
replaces pip and poetry

when run:

```bash
uv sync
```

1) creates virtual environment

2) install and synchronize dependencies
look at project config files, usually pyproject.toml and uv.lock file,
to see which packages required to run fastapi backend
then sync virtual environment

how to sync:
- install any missing packages
- update packages if lockfile has changed
- remove packages installed in environment but not listed in project config files

uv sync replaces the following:
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt