# Setuptools entry points
The most common way of exposing a Python CLI is to use the "scripts"
keyword in ``setup.py``.

```python
# file: setup.py
from setuptools import setup

setup(
  name='my_package',
  scripts=['scripts/my_cli'],
  ...
)
```

However, **entry points** represents an improved and cross-platform
approach.

```python
# file: setup.py
from setuptools import setup

setup(
  name='my_package',
  entry_points={
    'console_scripts': [
      'my_cli': 'my_package.cli:main'
    ]
  },
  ...
)
```

What's happens when the user installs the package is that ``pip`` will
make sure that ``my_cli`` is available as an executable on the system.
Once invoked, the ``main`` function of the ``my_package.cli`` module
will be called.

The problem with the former approach is that it requires separating
CLI related code into a isolated file outside the main package. With
**entry points** it's possible to unify all source code under the same
source package. This makes testing significantly easier.

---------------------

There's actually a lot more you can use entry points for. It is ideally
suited to act as a simple way for third party plugins to hook into your
application. A great example of such integration is employed by
[pytest][pytest] for their excellent plugin architecture.

You can also find out more in the [setuptools docs][setuptools].


[pytest]: http://pytest.org/latest/
[setuptools]: https://pythonhosted.org/setuptools/setuptools.html#automatic-script-creation
