===================
VIM Pdb integration
===================

Abstract
========

This package provides an integration of the Python debugger ``pdb`` into the
VIM editor.

Requirements
============

**vimpdb** requires a VIM that supports both ``python`` and ``clientserver`` options.

Find out if it is the case by issuing the following command at the VIM prompt::

    :version

If the options are supported, you will see ``+clientserver`` and ``+python`` in the
output. In the opposite case, you will see ``-clientserver`` or ``-python``.

On Linux and Windows, the default VIM build should be already server-enabled.
On Mac OS X, you'll want to use MacVIM_. MacVIM has also python compiled in by default.

.. _MacVIM: http://code.google.com/p/macvim/

Installation
============

Just install this package using ``easy_install`` or similar::

    $ easy_install vimpdb

Configuration
=============

You might need to setup the ``VIMPDB_VIMSCRIPT`` environment variable. It should hold
the command used at the shell prompt to launch a VIM supporting the options
mentioned above. (Default value is ``vimpdb``).

This script should also set the ``--servername`` option to specify a server
name.  You can think of this as a "window name" which is used to send remote
commands to -- this is how **vimpdb** communicates with a certain VIM instance.

Server Name
-----------

You might need to setup the ``VIMPDB_SERVERNAME`` environment variable. It should hold
the name of the VIM server you will be using. (Default value is ``VIMPDB``).  You may
list the currently running VIM servers using::

    $ vim --serverlist
    VIM

Or, on a Mac::

    $ /Applications/MacVim.app/Contents/MacOS/Vim --serverlist
    VIM

Note that the default ``servername`` is ``VIM``

Starting a VIM Server for Debugging
-----------------------------------

To start a VIM server for debugging, issue following command on the shell::

    $ vim --servername VIMPDB

Or, on a Mac, if you installed the ``mvim`` script::

    $ mvim --servername VIMPDB

When a VIM supporting ``clientserver`` option has started, you can find its name by issuing the
following command at the VIM prompt:

    :echo v:servername

Using
=====

Using **vimpdb** is easy -- just call ``set_trace`` as usual::

    import vimpdb; vimpdb.set_trace() 

Now, when the python interpreter hits that line, VIM will get the focus and
load the source file.

You may now use the following commands:

.. csv-table:: VimPDB Commands
    :header-rows: 1

    Key, Command
    n , Next
    s , Step
    a , Args
    u , Up
    d , Down
    r , Return
    c , Continue
    b , Sets a breakpoint at the line on which the cursor is sitting.
    w , Displays the value of the word on which the cursor is sitting.
    x , Switch to debugging with standard Pdb.
    v , Switch back to VimPdb from plain Pdb.

Standard Pdb hook
=================

If you find it hard to change habits and keep on typing 

::

    import pdb; pdb.set_trace()

you can add the following line to the  ``.pdbrc`` file sitting in your home
folder::

    import vimpdb; vimpdb.hookPdb()

This way, the command ``v(im)`` mentioned above is added to your standard Pdb
and you can switch to **vimpdb** at any time.

Known issues
============

* Currently, when you stop debugging, the buffers which you debugged with are
  left in an inconvenient state : the keys mapped to Pdb commands are still
  mapped. In other words, switching from debugging to fixing code is not
  convenient.

..  vim: set ft=rst ts=4 sw=4 expandtab tw=78 : 