# Project Structure

- **pyproject.toml**
- **license**
- **readme.md**
- **src/**
  - **package/**
    - `utils.py`
    - `main.py`
    - `__init__.py`
- **test/**
  - `test.py`

## Notes

1. **Python Package Path Resolution:**
   - Python looks for packages in `sys.path`, whose first entry is the directory containing your script.

2. **Non-Recursive Search in sys.path:**
   - The Python interpreter does not search recursively in `sys.path`.
   - Use Case: To import `utils.py` in `main.py`, you must include the path up to the `src` directory in `PythonPath`. Otherwise, the interpreter won't be able to find it.

3. **Relative Imports and Running Scripts Directly:**
   - Relative imports do not work when running a script directly because when a Python script is run, `__name__` is set to `__main__`, indicating it's the entry point of the application.
   - For example, the name for `utils` when imported is `src.package.utils`. However, if `utils.py` is run directly, the name becomes `__main__`, which is why relative imports won't work.
   - To make relative imports work when running `utils.py` directly, navigate to the `src` directory and run `python3 -m package.utils`.

4. **Structure for pyproject.toml File:**
   ```toml
   [build-system]
   requires = ["poetry-core>=1.0.0"]
   build-backend = "poetry.core.masonry.api"

   [tool.poetry]
   name = "package"
   version = "1.0.0"
   authors = ["Shubham Dogra <shubham@gmail.com>"]
   description = "A small example package"
   readme = "README.md"
   requires-python = ">=3.7"
   classifiers = [
       "Programming Language :: Python :: 3",
       "License :: OSI Approved :: MIT License",
       "Operating System :: OS Independent",
   ]

   [tool.poetry.dependencies]
   PyYAML = "^6.0"
   boto3 = "^1.26.135"
   requests = "^2.30.0"

   [tool.poetry.scripts]
   package = "package.main:run_cli"

   [tool.poetry.urls]
   "Homepage" = "https://github.com/pypa/sampleproject"
   "Bug Tracker" = "https://github.com/pypa/sampleproject/issues"
