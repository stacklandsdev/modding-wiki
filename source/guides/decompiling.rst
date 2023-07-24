Decompiling the game
####################

.. warning::
	PLEASE DO NOT SHARE EXTRACTED/DECOMPILED ASSETS PUBLICLY

Decompiling the game is the best way to learn about how certain features are implemented. This
guide will teach you how to use various tools to read the code of Stacklands. The code is compiled
into `assemblies <https://learn.microsoft.com/en-us/dotnet/standard/assembly/>`_, and can easily
be extracted.

Choosing a decompiler
=====================

There are various C# decompilers, each with their own benefits, though since the core feature set
is largely similar, the choice often comes down to preference.

* `ILSpy <https://github.com/icsharpcode/ILSpy>`_ (windows only) / `AvaloniaILSpy <https://github.com/icsharpcode/AvaloniaILSpy>`_ (cross-platform)
* `dnSpy <https://github.com/dnSpyEx/dnSpy>`_
* `dotPeek <https://www.jetbrains.com/decompiler/>`_

The rest of the guide will focus on ILSpy, but you can find all the showcased features in other tools.

Decompiling the code
====================

Open the ``GameScripts.dll`` file in ILSpy by either dragging it onto the window or finding it in
``File > Open``. The DLL file is found in ``<Path to Stacklands>/Stacklands_Data/Managed``. If you
are interested in other code, see the :ref:`File guide<File guide>` section.

After opening the DLL, it will appear in the panel on the left. Click ``GameScripts`` and ``-`` to
view the list of classes. You can click on any of them to view its code.

.. image:: https://user-images.githubusercontent.com/33525058/183427961-41be00df-8c18-4bf4-ae3c-58ac0d3697dd.png

Exporting the code
==================

You may export the code to get better integration with certain editors such as VSCode. This is
a completely optional step. Right click ``GameScripts`` and select ``Save Code``, then create
a folder where the code will be exported.

.. image:: https://user-images.githubusercontent.com/33525058/183428373-833d94a0-648b-4138-aec7-4a46bfee5e30.png

.. _File guide:

File guide
==========

The DLL files are found in ``<Path to Stacklands>/Stacklands_Data/Managed``.

.. list-table::

	* - ``GameScripts.dll``
	  - Contains all of the gameplay related code

	* - ``SokLoc.dll``
	  - Contains the code of the localization system