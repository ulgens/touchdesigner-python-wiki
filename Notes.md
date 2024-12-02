# Get Python executable path

```python
import sys
sys.executable
# '/Applications/TouchDesigner.app/Contents/MacOS/TouchDesigner'
```

# Get installed packages with version info

```python
import sys
from importlib.metadata import PackageNotFoundError
from tabulate import tabulate

show_na_versions = False

data = []

for name, module in sys.modules.items():
    try:
        version = module.__version__
    except (AttributeError, KeyError, PackageNotFoundError):
        if show_na_versions:
            version = "-"
        else:
            continue
    data.append([name, version])

table = tabulate(
    sorted(data, key=lambda x: x[0]),
    headers=["Module", "Version"],
)

print(table)
```
