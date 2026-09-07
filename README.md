# **UV Python Project Setup**

A quick guide to installing **uv**, creating a Python project, managing a virtual environment, installing packages, and synchronizing dependencies.

---

## **1. Install uv**

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

## **2. Initialize a Project**

Create a new project using `uv`:

```bash
uv init my-project
```

Move into the project directory:

```bash
cd my-project/
```

---

## **3. Create a Virtual Environment**

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

## **4. Activate the Virtual Environment**

Activate the virtual environment:

```bash
source .venv/bin/activate
```

Your terminal prompt should now show the virtual environment name:

```text
(my-project) harman@Harman-MacBook-Pro my-project %
```

---

## **5. Verify the Python Environment**

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

### **⚠️ Important**

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

## **6. Add Python Packages**

Use `uv add` to install packages.

For example, to install NumPy:

```bash
uv add numpy
```

This will:

* Add NumPy to `pyproject.toml`
* Update `uv.lock`
* Install NumPy into the project's environment

### **`uv pip install`**

You can also install packages using:

```bash
uv pip install numpy
```

This works similarly to:

```bash
pip install numpy
```

It installs NumPy into the current virtual environment, but **does not add NumPy to `pyproject.toml`**.

### **For a uv project, prefer:**

```bash
uv add numpy
```

**Remember:**

* `uv add numpy` → Add NumPy as a **project dependency**
* `uv pip install numpy` → Install NumPy directly into the **environment**

Test the installation:

```bash
python -c "import numpy; print(numpy.__version__)"
```

You can also use:

```bash
uv run python -c "import numpy; print(numpy.__version__)"
```

---

## **7. Sync Project Dependencies**

`uv sync` synchronizes your virtual environment with the dependencies defined in `pyproject.toml` and recorded in `uv.lock`.

Run:

```bash
uv sync
```

This ensures that your environment has the dependencies required by the project.

### **When to use `uv sync`**

Use `uv sync` when:

* You clone an existing `uv` project from GitHub
* `pyproject.toml` or `uv.lock` has changed
* You want to make sure your environment matches the project dependencies
* You create a fresh `.venv`

For example, after cloning a project:

```bash
git clone <repository-url>
cd my-project
uv sync
```

`uv` will create/update the project's `.venv` and install the required dependencies.

### **Simple way to remember**

```text
uv add     → Add a new dependency to the project
uv sync    → Make the environment match the project
uv run     → Run something using the project environment
```

---

## **8. Add More Packages**

For example:

```bash
uv add pandas
```

Multiple packages can be installed together:

```bash
uv add numpy pandas requests
```

After adding packages, `uv` automatically updates `pyproject.toml` and `uv.lock`.

You can also manually synchronize the environment:

```bash
uv sync
```

---

## **9. Run Python**

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

## **10. Deactivate the Virtual Environment**

When you're finished working:

```bash
deactivate
```

The `(my-project)` prefix should disappear from your terminal.

---

## **11. Recommended Workflow**

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

# Synchronize dependencies
uv sync

# Run Python
python

# Deactivate when finished
deactivate
```

---

## **12. Quick UV Command Reference**

| Command                     | Purpose                                               |
| --------------------------- | ----------------------------------------------------- |
| `uv init my-project`        | Create a new Python project                           |
| `uv venv`                   | Create a virtual environment                          |
| `uv venv --python 3.14.7`   | Create a venv with a specific Python version          |
| `source .venv/bin/activate` | Activate the virtual environment                      |
| `uv add numpy`              | Add NumPy as a project dependency                     |
| `uv pip install numpy`      | Install NumPy directly into the environment           |
| `uv sync`                   | Synchronize the environment with project dependencies |
| `uv run python`             | Run Python using the project environment              |
| `uv run main.py`            | Run a Python file using the project environment       |
| `deactivate`                | Deactivate the virtual environment                    |

---

### **Key Things to Remember**

> **`uv add` → Add a dependency to the project**

> **`uv sync` → Synchronize the environment with the project**

> **`uv run` → Run commands using the project environment**

> **`uv pip install` → Install directly into the environment**

### **Expected `which python`**

```text
/Users/harman/agentic-ai/my-project/.venv/bin/python
```

The key thing to remember is:

> **When the virtual environment is activated, `which python` should point to `.venv/bin/python`.**

### Add Dependencies from requirements.txt

If you already have a requirements.txt file and want to add all its packages to your uv project, use:

```bash
uv add -r requirements.txt
```

For example, if requirements.txt contains:

pydantic
fastapi

This will:

Add the packages to pyproject.toml
Update uv.lock
Install the dependencies into the project's environment
