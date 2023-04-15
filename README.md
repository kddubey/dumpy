# DumPy

Dump of dumb Python code which was once useful.

<details>
<summary>sphinx_setup.py</summary>

[Sphinx](https://www.sphinx-doc.org/en/master/) is super awesome.

I wrote this script which automatically sets up documentation in a style that's to my
liking. My preferences are:
  * Separate source and build directories, because this structure is the one which the
    Read the Docs builder
    [assumes](https://docs.readthedocs.io/en/stable/tutorial/#preparing-your-project-on-github).
  * No "Submodule ..." or "Subpackage ..." headers, as these should be abstracted to the
    user
  * The code `[source]` button should link to the code in GitHub
      * I'm surprised at how much Googling (and some unsuccessful ChatGPT-ing) I had to
        do to find a bit-sized implementation of this. Big thanks to [this GitHub
        comment](https://github.com/readthedocs/sphinx-autoapi/issues/202#issuecomment-907582382)
  * Arguments in function signatures should be separated by newlines
  * Use the [PyData Sphinx
    Theme](https://pydata-sphinx-theme.readthedocs.io/en/stable/index.html)
  * Use [NumPy
    docstrings](https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html).
    The default style is less readable as a developer and as a user (when I just wanna
    hover the code instead of opening up the documentation in my browser)
  * Use the `{package}.rst` file in the index, drop `modules.rst`.

Modify the global variables at the top of the script. Use at your own risk.
</details>


<details>
<summary>wrap</summary>

Decorators which automate some things about docstrings and function annotations. They
dynamically modify the function's `__doc__` and `__annotations__` attributes, so static
code analyzers unfortunately won't reflect the modifications. After using these
decorators, I realized that I rely a lot on the docstrings that static code analyzers
show me. I assume other users do to. So I opted for copy-pasting parts of docstrings
instead of using these automations.
</details>


<details>
<summary>type_str</summary>

Calling `.info()` or `.dtypes` on a dataframe is a typical step before starting any data
analysis. But the outputs can be uninformative for data pulled from Postgres. Arrays are
converted to lists, and JSONBs are converted to dictionaries. And these get the
uninformative type `object` when pandas checks data types. Moreover, even if you knew
certain columns were lists or dicts, you can't know what they contain without manually
coding some datatype checks yourself.

`type_str` gives accurate and more precise data types in the style of type hints. Use it
by running `df.apply(type_str)` in place of `df.dtypes`. You can actually use it to peek
into any opaque iterable. Note that it's recursive and scales poorly, so use at your own
risk :-) 
</details>
