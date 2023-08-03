Extracting the Game's Assets
############################

.. warning::
	PLEASE DO NOT SHARE EXTRACTED/DECOMPILED ASSETS PUBLICLY

Extracting the game's assets is an easy way to find out how certain features are implemented and what properties built-in cards have.

Setting up AssetRipper
======================

Download the latest version of AssetRipper for your operating system from `here <https://github.com/AssetRipper/AssetRipper/releases>`_, extract it, and launch ``AssetRipper.exe``.

Extracting assets
=================

You can leave all the settings on default to export most of the interesting assets.

If you want to let AssetRipper decompile the game's code, set "Script Export Format" to "Decompiled".
If you don't want to decompile the code (e.g. because you're using one of the methods described in :doc:`Decompiling guide <./decompiling>`), set "Script Content Level" to "Level 0". This will speed up the extraction a bit.

Next, lick ``File -> Open Folder`` and select the ``Stacklands`` or ``Stacklands_Data`` folder. You can find them by right-clicking on the game
on Steam, selecting ``Manage``, and then ``Browse Local Files``.

By default, the directory will be ``C:\Program Files (x86)\Steam\steamapps\common\Stacklands`` on Windows, ``~/Library/Application Support/Steam/steamapps/common/Stacklands`` on Mac, and ``~/.steam/steam/SteamApps/common/Stacklands`` on Linux.

AssetRipper will now start extracting the assets. This may take a few minutes. You can then browse and extract individual assets directly in AssetRipper
or just export everything using the ``Export`` menu. Exporting everything allows you to easily search through the exported files and let's you easily view other assets without having to use AssetRipper again.

All the interesting assets are in ``globalgamemanagers/ExportedProject/Assets`` in the resulting folder. Most of the extracted files will appear twice, one with a ``.meta`` extension. You can ignore those.

Important assets
================

All the paths are relative to the ``globalgamemanagers/ExportedProject/Assets`` directory.

.. list-table::

	* - ``Resources/cards``
	  - Contains all the cards in the game. The cards start with their card type. ``Blueprint_`` represent ideas which also specify how something is crafted.

	* - ``Scripts/GameScripts``
	  - Contains the decompiled code of the game (if you didn't disable decompilation in the settings)

Figuring out the script of a card
=================================

It's often useful to know which script type a card uses so you can either use the same one for your own card or read the corresponding code to find out how it works.
Unfortunately, the card assets don't contain the name of the script directly. Instead, they reference the script via a number::

	m_Script: {fileID: 11500000, guid: 42230d90d2ff7d5f798f23c6db20eea5, type: 3}

But it's possible to find the script corresponding to this id. To do that, search for the ``guid`` value in the extracted ``Scripts`` directory (this requires that you enabled decompilation in the export settings).
You will find a file containing the guid value. The name of the file tells you the name of the script. On Mac and Linux, a simple way to search through all files is to use ``grep -R``::

	grep -R 42230d90d2ff7d5f798f23c6db20eea5 Scripts

This gives the following result::

	Scripts/GameScripts/Demon.cs.meta:guid: 42230d90d2ff7d5f798f23c6db20eea5

The first part is the file name, so the script is ``Demon``. You can check the corresponding file without the ``.meta`` extension to see its code.
