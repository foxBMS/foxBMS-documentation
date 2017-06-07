.. include:: ../../macros.rst



.. _software_documentation_build:

======================
Software Build Process
======================


Requirements
------------

The build process of |foxbms| heavily depends on Python, for example, for code
generation purposes. |foxbms| hence comes with its own Python distribution,
called |foxconda|, powered by `Anaconda <https://continuum.io>`_. These build
instructions assume that |foxconda| was successfully installed and that the
``PATH`` environment has been adjusted accordingly. For further information
refer to the |foxconda| documentation.

Obtaining the Sources
---------------------

The |foxbms| sources are cloned/pulled by the |foxbms| bootstrap step. This step
is performed by ``python bootstrap.py``.
After that step the directory structure in ``foxBMS-setup`` directory should
look like:

.. code-block:: none

  foxBMS-setup <dir>
  |__.git <dir> (*)
  |__build <dir>
  |__foxBMS-documentation <dir>
  |__foxBMS-hardware <dir>
  |__foxBMS-primary <dir>
  |__foxBMS-secondary <dir>
  |__foxBMS-tools <dir>
  |__FreeRTOS <dir>
  |__hal <dir>
  |
  |__.gitignore <file> (*)
  |__bootstrap.py <file>
  |__build.py <file>
  |__CHANGELOG.md <file>
  |__clean.py <file>
  |__LICENSE.md <file>
  |__README.md <file>
  |__wscript <file>


(*) Directories and files with starting full stop are hidden in Windows in default
configuration.

Build
-----
|foxbms| targets can be build using the command line or using the |foxbms|
FrontDesk. This section describes the build from command line.

The script for building targets is in |foxbms|-setup and called ``build.py``.
A help is available by ``python build.py -h``.

In |foxbms| can build several targets, the output is stored in a subdirectory of
/build. These are

 - Primary MCU:

  - Doxygen documentation

   - This target is build by ``python build.py -p --doxygen``.
   - The output directory is ``/build/primary/doxygen``.
   - The main document of the software documentation is found at
     ``build\primary\doxygen\html\index.html``.

  - Binaries

   - This target is build by ``python build.py -p``.
   - The output directory is ``build/primary/foxBMS-primary/``.
   - This includes in directory ``build/primary/foxBMS-primary/src/general``:
     ``foxbms.elf``, ``foxbms_flash.bin``, ``foxbms_flashheader.bin``
     and ``foxbms.hex``.

 - Secondary MCU:

  - Doxygen documentation

   - This target is build by ``python build.py -s --doxygen``.
   - The output directory is ``/build/secondary/doxygen``.
   - The main document of the software documentation is found at
     ``build\secondary\doxygen\html\index.html``.

  - Binaries

   - This target is build by ``python build.py -s``.
   - The output directory is ``build/secondary/foxBMS-secondary/``.
   - This includes in directory ``build/secondary/foxBMS-secondary/src/general``
     : ``foxbms.elf``, ``foxbms_flash.bin``, ``foxbms_flashheader.bin``
     and ``foxbms.hex``.

 - General documentation

  - Sphinx documentation

   - This target is build by ``python build.py --sphinx``.
   - The output directory is ``build/sphinx/``.
   - The main document of the software documentation is found in
     ``build/sphinx/foxBMS-documentation/doc/sphinx/html/index.html``.

Clean
-----
|foxbms| targets can be cleaned using the command line or using the |foxbms|
FrontDesk. This section describes the clean from command line.

The script for cleaning targets is in |foxbms|-setup and called ``clean.py``.
A help is available by ``python clean.py -h``.

All targets described in build can also be cleaned.

Cleaning targets:
 - Primary: ``python clean.py -p``: cleans primary binaries and Doxygen
   documentation.
 - Secondary: ``python clean.py -s``: cleans secondary binaries and Doxygen
   documentation.
 - General documentation: ``python clean.py --sphinx``: cleans the Sphinx
   documentation.