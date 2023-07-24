Localization
############

Stacklands has a built-in localization system in the form of the ``SokLoc`` class, the source code
of which can be found in ``SokLoc.dll``. You should use localization for your mod even if you only
provide translations for a single language, because other modders can easily create translation
mods for yours.

Creating your localization document
===================================

Localization documents are in `TSV format <https://en.wikipedia.org/wiki/Tab-separated_values>`_, which
you can easily create using Google Sheets or Excel.

The first row of the document should look like this:

.. code-block::

	Term | Notes | English | Dutch | ...

.. note::

	You do not need to make columns for languages you don't provide translations for! They will automatically fall back to the English column.

Make sure your terms are unique, prefixing them with your mod's ID is an easy way to ensure this.

.. image:: https://user-images.githubusercontent.com/33525058/182152402-2bab35bc-d1b4-4dee-91a9-57b84bc0b99c.png

Loading your localization document into the game
================================================

If there is a ``localization.tsv`` file in your mod's folder, the game will automatically load it.
You can also load any file using the ``SokLoc.LoadTermsFromFile()`` method, like so:

.. code-block:: c#
	:linenos:

	SokLoc.instance.LoadTermsFromFile("D:/example.tsv");
	SokLoc.instance.LanguageChanged += () => // make sure to reload the file when the language is changed
	{
		SokLoc.instance.LoadTermsFromFile("D:/example.tsv");
	};

Using SokLoc
============

To get a translated string, use the ``SokLoc.Translate`` method:

.. code-block:: c#
	:linenos:

	SokLoc.Translate("yourmod_test"); // "very epic string"
	SokLoc.instance.SetLanguage("Dutch"); // YOU SHOULD NOT CALL THIS METHOD DIRECTLY! it gets called via the settings menu and is only used here as an example
	SokLoc.Translate("yourmod_test"); // "zeer epische text"

Using LocParams
===============

The localization system provides a very easy for handling variables in strings. By surrounding text with
``[]``, it's handled as a variable. Example: ``wow, an [epic_param]!``.

.. code-block:: c#
	:linenos:

	SokLoc.Translate("yourmod_param_test", LocParam.Create("epic_param", "apple")); // "wow, an apple!"
	// wow, an [param1] and an [param2]!
	SokLoc.Translate("yourmod_params_test", LocParam.Create("param1", "apple"), LocParam.Create("param2", "orange")); // "wow, an apple and an orange!"

Using plurals
=============

The localization system provides an easy way for handling cases where a string should be translated
differently based on a variable number. You can seperate the singular and plural forms by prefixing
them with ``<one>`` and ``<other>``. Example: ``<one>give me one more coin<other>give me [count] more coins``.

.. code-block:: c#
	:linenos:

	SokLoc.Translate("yourmod_plural_test", LocParam.Plural("count", 1)); // "give me one more coin"
	SokLoc.Translate("yourmod_plural_test", LocParam.Plural("count", 3)); // "give me 3 more coins"

Exporting your document in TSV format
=====================================

Excel
-----

``File > Save As`` and select ``Tab Separated Value (.txt)`` as the format.

.. note::
	Don't forget to change the file extension to ``.tsv``!

.. note::
	Excel may add an empty line to the end of the file, which can cause Stacklands to parse it improperly. If this is the case, simply remove the last empty line in the file.

Google Sheets
-------------

``File > Download > Tab Seperated values (.tsv)``.

.. image:: https://cdn.discordapp.com/attachments/999288683167485982/1128726621751365783/image.png