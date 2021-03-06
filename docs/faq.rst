FAQ & Known issues
==================

Numpy problems
--------------

UCSF Chimera bundles its own distribution of some popular packages, like
``numpy``, and those are loaded before your env packages for compatibility
reasons. Be warned if you use specific versions for your project,
because you can face strange bugs if you don’t take this into account.

In some platforms (Linux), this can be worked around with some work on
the precendence of paths in ``sys.path``, but in some of them is not as easy (OS X).
The easiest and most robust way to fix this is by upgrading UCSF Chimera's ``numpy``:

::

    pip install --upgrade numpy -t "$(pychimera --path)/lib/python2.7/site-packages"

Take into account that this action will prevent outdated extensions from working again. As a far as we know, these are affected, but there might be more (please report it so we can update this list!):

- MMTK-dependent extensions: MD, Energy minimization
- AutoDock-dependent extensions: AutoDock Vina

If you use those often enough, you should have a separate, unmodified UCSF Chimera installation.

PyChimera GUI has ugly fonts
----------------------------

Anaconda-provided ``tk`` package is not built with truetype support (for several reasons; read `here <https://github.com/ContinuumIO/anaconda-issues/issues/776>`_ and `here <https://github.com/ContinuumIO/anaconda-issues/issues/6833>`_). Chimera does ship its own one (with correct font support), but since PyChimera loads its own Python interpreter, it ends up being replaces with ``conda``'s one. All ``conda`` environments are created with ``tk`` by default, so if the fonts really bother you, you can uninstall it with ``conda remove --force tk`` and it will fallback to system's one if needed.

Setuptools problems
-------------------

If you are using the development versions of ``pychimera``, Chimera's ``setuptools`` will
complain about the versioning scheme (ie, ``pychimera==0.1.11+6.gc2e1fbb.dirty``). As before,
the fix is to upgrade the package. You might have to remove it manually beforehand, though:

::

    rm -r $(pychimera --path)/lib/python2.7/site-packages/setuptools-3.1*
    pip install --upgrade setuptools -t "$(pychimera --path)/lib/python2.7/site-packages"
