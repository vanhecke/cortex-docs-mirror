---
description: >-
  Run linters to catch common programming errors, stylistic errors, and possible
  security issues
---

# Linting

As part of the build process, we run linters to catch common programming errors, stylistic errors, and possible security issues. Linters are run only when working with the package (directory) structure.

All linters are run via the [pre-commit](https://app.gitbook.com/s/nozw5MT5S8KZD2eF8roV/demisto-sdk-guide/demisto-sdk-commands/pre-commit) command.

{% hint style="info" %}
### Note

This script is also used to run pytest. See: [Unit Testing](unit-testing)
{% endhint %}

An example of the result from running pre-commit checks on the HelloWorld package:

```programlisting
Running pre-commit using template /Users/sfainberg/dev/demisto/content/.pre-commit-config_template.yaml
Running pre-commit with Python 3.11 on:
Packs/HelloWorld/Integrations/HelloWorld/HelloWorld.py
Packs/HelloWorld/Integrations/HelloWorld/HelloWorld.yml
Packs/HelloWorld/Integrations/HelloWorld/HelloWorld_description.md
Packs/HelloWorld/Integrations/HelloWorld/HelloWorld_image.png
Packs/HelloWorld/Integrations/HelloWorld/HelloWorld_test.py
Packs/HelloWorld/Integrations/HelloWorld/README.md
Packs/HelloWorld/Integrations/HelloWorld/command_examples
Packs/HelloWorld/Integrations/HelloWorld/test_data/get_alert.json
Packs/HelloWorld/Integrations/HelloWorld/test_data/incident_note_list_command.json
Packs/HelloWorld/Integrations/HelloWorld/test_data/ip_reputation.json
check json...............................................................Passed
check yaml...............................................................Passed
check python ast.........................................................Passed
check for merge conflicts................................................Passed
debug statements (python)................................................Passed
python tests naming......................................................Passed
check for added large files..............................................Passed
check for case conflicts.................................................Passed
poetry-check.........................................(no files to check)Skipped
pycln....................................................................Passed
ruff-py3.11..............................................................Passed
autopep8.................................................................Passed
mypy-py3.11..............................................................Passed
xsoar-lint...............................................................Passed
pylint-in-docker-demisto/python3:3.11.10.115186..........................Passed
pytest-in-docker-demisto/python3:3.11.10.115186..........................Passed
validate-deleted-files...................................................Passed
validate-content-paths...................................................Passed
validate-conf-json...................................(no files to check)Skipped
validate.................................................................Passed
secrets..................................................................Passed
merge-pytest-reports.....................................................Passed
coverage-pytest-analyze..................................................Passed
```

**Flake8**

[Flake8](https://flake8.pycqa.org/en/latest/) is a basic linter. It can be run without having all the dependencies available and will catch common errors. We also use this linter to enforce the standard python pep8 formatting style. On rare occasions you may encounter a need to disable an error/warning returned from this linter. To disable, add an inline comment on the line where you want to disable the error:

```programlisting
#  noqa: <error-id>
```

For example:

```programlisting
example = lambda: 'example'  # noqa: E731
```

When adding an inline comment always also include the error code you are disabling for. If there are other errors on the same line they will be reported. For more information, see [In-line Ignoring Errors](https://flake8.pycqa.org/en/latest/user/violations.html#in-line-ignoring-errors).

**Pylint**

[Pylint](https://pypi.org/project/pylint/) is similar to flake8 but is able to catch additional errors. We run this linter with error reporting only. It requires access to dependent modules and thus we run it within a Docker image similar with all dependencies (similar to how we run pytest unit tests). On rare occasions you may encounter a need to disable an error/warning returned from this linter. Disable by adding an inline comment on the line where you want to disable the error:

```programlisting
# pylint: disable=<error-name>
```

For example:

```programlisting
a, b = ... # pylint: disable=unbalanced-tuple-unpacking
```

You can also disable and then enable a block of code. For example (taken from `CommonServerPython.py`):

```programlisting
# pylint: disable=undefined-variable
if IS_PY3:
    STRING_TYPES = (str, bytes)  # type: ignore
    STRING_OBJ_TYPES = (str)
else:
    STRING_TYPES = (str, unicode)  # type: ignore
    STRING_OBJ_TYPES = STRING_TYPES  # type: ignore
# pylint: enable=undefined-variable
```

{% hint style="info" %}
### Note

Pylint can take both the error name and error code when doing inline comment disables. We recommend using the name, which is clearer to understand.
{% endhint %}

For more information, see [messages control](https://pylint.readthedocs.io/en/latest/user_guide/messages/message_control.html).

For classes that generate members dynamically (such as goolgeapi classes) pylint generates multiple `no-member` errors as it can't detect the members of the class. In this case, we recommend adding a `.pylintrc` file which includes the following:

```programlisting
[TYPECHECK]

ignored-classes=<Class Name List>
```

For an example of ignored-classes, see [here](https://github.com/demisto/content/blob/fe2bd5cddc6e521e08ef65fcd456a4214f8c4d93/Integrations/Gmail/.pylintrc).

**mypy**

[mypy](https://mypy-lang.org/) uses type annotations to check code for common errors. It contains type information for many popular libraries (via typeshed project). Additionally, it allows you to define type annotations for your own functions and data structures. Type annotations are fully supported as a language feature in Python 3.6 and above. In earlier versions, type annotations are provided via the use of comments.

We run mypy in a relatively aggressive mode, and it also type checks functions which don't contain type definitions. In some cases, this may cause additional errors. You can ignore errors, if needed, with an inline comment:

```programlisting
# type: ignore[<error-name>]
```

For example:

```programlisting
a = 1
b = "2"
a = b  # type: ignore[assignment]
```

{% hint style="info" %}
### Note

Mypy introduced the ignore\[\<error-name>] syntax in version 0.730. See [Error code docs](https://mypy.readthedocs.io/en/latest/error_codes.html). You might also see in the code ignores such as `type: ignore` without the `error-name`. This is usually from older code written before the support for `error-name` ignores. We do not recommend using this ignore style as it ignores all errors and increases the risk of ignoring unexpected serious errors.
{% endhint %}

If you receive a `Need type annotation error`, we recommend defining the type of the variable which is missing type annotation, instead of adding an `ignore` comment. This error is usually received when an empty dict or list is defined and mypy can not infer the type of the object. In this case, it is better to define the type as **dict** or **list**:

```programlisting
my_list: list = []
```

If you know the type that the list will hold, use the type constructor `list` that can specify also what type it holds. For example a list that we know that will hold strings:

```programlisting
my_list: list[str] = []
```

{% hint style="info" %}
### Note

When using type besides `list`, `dict`, `str`, `int`, `tuple`, you need to import the type from the `typing` module.
{% endhint %}

Read more about [mypy](https://mypy.readthedocs.io/en/latest/index.html).

**Bandit**

[Bandit](https://github.com/PyCQA/bandit) is a tool designed to find common security issues in Python code.

We run bandit with a confidence level of HIGH. In the rare case that it reports a false positive, you can exclude the code by adding a comment: `# nosec`. For more information, see: [https://github.com/PyCQA/bandit#exclusions](https://github.com/PyCQA/bandit#exclusions).

**XSOAR linter**

This is a custom linter, based on pylint, whose main purpose is to catch errors regarding Cortex XSIAM code standards. The linter is activated using the pylint load plugins ability. We run this linter only with custom Cortex XSIAM error and warning messages (all other messages are disabled). On rare occasions, you may encounter a scenario in which you need to disable an error or warning message from being returned by the XSOAR linter. To do this add an inline comment, as shown below, on the line where you want to disable the error:

```programlisting
# pylint: disable=<error-name>
```

For example:

```programlisting
print('Success!') # pylint: disable=print-exists
```

You can also disable and then enable a block of code. The following example is taken from `CommonServerPython.py`:

```programlisting
# pylint: disable=sys-exit-exists
if IS_PY3:
    pass
else:
    sys.exit(1)
# pylint: enable=sys-exit-exists
```

{% hint style="info" %}
### Note

Pylint can take both the error name and error code when using an inline comment disable message. We recommend using the error name instead of the error code, as it is easier to understand.
{% endhint %}
