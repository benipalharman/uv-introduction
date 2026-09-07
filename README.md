# UV Python Project Setup

A quick guide to installing **uv**, creating a Python project, managing a virtual environment, and installing packages.

## 1. Install uv

Install `uv` using the official installation script:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

OR

```bash
brew install uv
```

Verify the installation:

```bash
uv --version
```

---

## 2. Initialize a Project

Create a new project using `uv`:

```bash
uv init my-project
```

Move into the project directory:

```bash
cd my-project/
```

---

## 3. Create a Virtual Environment

Create the virtual environment:

```bash
uv venv --python 3.14.7
```

> You can omit `--python 3.14.7` if you want `uv` to automatically select the Python version.

This creates a `.venv` directory:

```text
my-project/
├── .venv/
├── pyproject.toml
├── README.md
└── ...
```

---

## 4. Activate the Virtual Environment

Activate the virtual environment:

```bash
source .venv/bin/activate
```

Your terminal prompt should now show the virtual environment name:

```text
(my-project) harman@Harman-MacBook-Pro my-project %
```

---

## 5. Verify the Python Environment

Check which Python is being used:

```bash
which python
```

The output **should point to `.venv/bin/python`**:

```text
/Users/harman/agentic-ai/my-project/.venv/bin/python
```

The important part is:

```text
.venv/bin/python
```

You can also verify the Python version:

```bash
python --version
```

Expected:

```text
Python 3.14.7
```

### ⚠️ Important

If `which python` points somewhere else, such as:

```text
/opt/homebrew/bin/python3
```

or:

```text
/Users/harman/opt/anaconda3/bin/python
```

then your terminal is **not using the project's virtual environment**.

---

## 6. Add Python Packages

Use `uv add` to install packages.

For example, to install NumPy:

```bash
uv add numpy
```

This will:

* Add NumPy to `pyproject.toml`
* Update `uv.lock`
* Install NumPy into the project's environment

OR

```bash
uv pip install numpy
```

* Installs NumPy into the current virtual environment.
* uv pip install numpy It works similarly to: pip install numpy
* Important :: uv pip install numpy installs NumPy in the environment, but does not add NumPy to pyproject.toml.

# For a uv project, prefer:

```bash
uv add numpy
```

Test the installation:

```bash
python -c "import numpy; print(numpy.__version__)"
```

You can also use:

```bash
uv run python -c "import numpy; print(numpy.__version__)"
```

---

## 7. Add More Packages

For example:

```bash
uv add pandas
```

Multiple packages can be installed together:

```bash
uv add numpy pandas requests
```

---

## 8. Run Python

With the virtual environment activated:

```bash
python
```

Then:

```python
import numpy

print(numpy.__version__)
```

Alternatively, without activating the environment:

```bash
uv run python
```

---

## 9. Deactivate the Virtual Environment

When you're finished working:

```bash
deactivate
```

The `(my-project)` prefix should disappear from your terminal.

---

## 10. Recommended Workflow

For a new project, the typical workflow is:

```bash
# Create project
uv init my-project

# Enter project
cd my-project/

# Create virtual environment
uv venv --python 3.14.7

# Activate environment
source .venv/bin/activate

# Verify environment
which python
python --version

# Add packages
uv add numpy

# Run Python
python

# Deactivate when finished
deactivate
```

### Expected `which python`

```text
/Users/harman/agentic-ai/my-project/.venv/bin/python
```

The key thing to remember is:

> **When the virtual environment is activated, `which python` should point to `.venv/bin/python`.**
