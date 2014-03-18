.. image:: https://secure.travis-ci.org/kilink/ghdiff.png?branch=master
   :target: http://travis-ci.org/kilink/ghdiff

.. image:: https://coveralls.io/repos/kilink/ghdiff/badge.png
   :target: https://coveralls.io/r/kilink/ghdiff

ghdiff
======

Generate Github-style HTML for unified diffs.

Note, this is the "class" version of the original "ghdiff" package.
It provides an easily overridable class, but the behavior is the same as the
original package from Patrick Strawderman ("kilink")

Install
=======

.. code:: bash

    pip install ghdiff_class


diff
====

Generate a diff and output Github-style HTML for it.

.. code-block:: pycon

    >>> from ghdiff import GHDiff
    >>> from six import print_
    >>> print_(GHDiff.diff("a\nb", "b\nb"))
    <style type="text/css">
    ...
    </style>
    <div class="diff">
        <div class="control">@@&nbsp;-1,2&nbsp;+1,2&nbsp;@@
        </div>
        <div class="delete">-a</div>
        <div class="">&nbsp;b</div>
        <div class="insert">+b</div>
    </div>

The css option controls whether or not the output includes CSS.

.. code-block:: pycon

    >>> print_(GHDiff.diff("blah blah blah\nb", "blah zxqq blah\nb", css=False))
    <div class="diff">
        <div class="control">@@&nbsp;-1,2&nbsp;+1,2&nbsp;@@
        </div>
        <div class="delete">-blah&nbsp;<span class="highlight">blah</span>&nbsp;blah</div>
        <div class="insert">+blah&nbsp;<span class="highlight">zxqq</span>&nbsp;blah</div>
        <div class="">&nbsp;b</div>
    </div>

diff accepts lists of strings representing lines as well.

.. code-block:: pycon

    >>> print_(GHDiff.diff(["blah blah blah", "b"], ["blah zxqq blah", "b"]))
    <style type="text/css">
    ...
    </style>
    <div class="diff">
        <div class="control">@@&nbsp;-1,2&nbsp;+1,2&nbsp;@@
        </div>
        <div class="delete">-blah&nbsp;<span class="highlight">blah</span>&nbsp;blah</div>
        <div class="insert">+blah&nbsp;<span class="highlight">zxqq</span>&nbsp;blah</div>
        <div class="">&nbsp;b</div>
    </div>

colorize
========

colorize takes an existing unified diff and outputs Github-style markup.

.. code-block:: pycon

    >>> print_(GHDiff.colorize("""\
    ... index 921100e..8b177e1 100755
    ... --- a/src/ghdiff.py
    ... +++ b/src/ghdiff.py
    ... @@ -10,20 +10,24 @@ def escape(text):
    ...  default_css = \"\"\"\
    ...  <style type="text/css">
    ...  %s
    ... -</style>\"\"\" % (open(os.path.join(os.path.dirname(__file__), "default.css")).read(),)
    ... +</style>
    ... +\"\"\" % (open(os.path.join(os.path.dirname(__file__), "default.css")).read(),)
    ... +"""))
    <style type="text/css">
    ...
    </style>
    <div class="diff">
    <div class="control">@@&nbsp;-10,20&nbsp;+10,24&nbsp;@@&nbsp;def&nbsp;escape(text):</div>
    <div class="">&nbsp;default_css&nbsp;=&nbsp;"""&nbsp;&lt;style&nbsp;type="text/css"&gt;</div>
    <div class="">&nbsp;%s</div>
    <div class="delete">-&lt;/style&gt;"""&nbsp;%&nbsp;(open(os.path.join(os.path.dirname(__file__),&nbsp;"default.css")).read(),)</div>
    <div class="insert">+&lt;/style&gt;</div>
    <div class="insert">+"""&nbsp;%&nbsp;(open(os.path.join(os.path.dirname(__file__),&nbsp;"default.css")).read(),)</div>
    <div class="insert">+</div>
    </div>
