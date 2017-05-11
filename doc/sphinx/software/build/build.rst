Build
=====

.. include:: ./macros.rst

Requirements
------------

The build process of |foxbms| heavily depends on Python, for example, for code generation purposes. |foxbms| hence comes with its own Python distribution, called |foxconda|, powered by `Anaconda <https://continuum.io>`_. These build instructions assume that |foxconda| was successfully installed and that the ``PATH`` environment has been adjusted accordingly. For further information refer to the |foxconda| documentation.

Obtaining the sources
---------------------

FIXME GitHub instruction are to follow.


Build
-----

``python tools/waf-1.8.12 configure --check-c-compiler=gcc build``
