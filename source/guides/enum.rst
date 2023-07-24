Extending Enums
###############

This guide will introduce you to the :code:`EnumHelper` class, and will provide
examples for extending various enums found in the game.

The EnumHelper module is fully generic, and works with any enum, even those which
are not part of the vanilla game. Consider the following code:

.. highlight:: c#
.. code-block::
	:linenos:

	enum Shapes
	{
		Circle,
		Triangle
	}

	class Shape
	{
		public Shapes Type;

		public Shape(Shapes type)
		{
			this.Type = type;
		}
	}

	var circle = new Shape(Shapes.Circle);
	Logger.Log($"circle type is ${circle.Type}");
	//> circle type is Circle

The above code snippet creates a circle shape, however, it can only be a circle or a triangle,
what if we wanted a square? For this, we can use the :code:`EnumHelper.ExtendEnum` function, like so:

.. highlight:: c#
.. code-block::
	:linenos:
	:lineno-start: 20

	int squareValue = EnumHelper.ExtendEnum<Shapes>("Square"); // this function returns the corresponding integer
	var square = new Shape(squareValue);
	Logger.Log($"square type is ${square.Type}");
	//> square type is 2
	// Circle = 0, Triangle = 1, Square = 2

	// we can also get the type name by using EnumHelper.GetName()
	Logger.Log($"square type is ${EnumHelper.GetName<Shapes>(squareValue)}");
	//> square type is Square


Example: Creating A Custom CardType
===================================

If your mod adds custom cards, you may also want to create custom types for some of them. Simply extend the ``CardType``
enum in your mods Awake method (see `Awake or Ready? <awake-ready.html>`_), so it runs before the cards are loaded.


.. code-block:: c#
	:linenos:

	private void Awake()
	{
		int customCardType = EnumHelper.ExtendEnum<CardType>("CustomCardType");
		// use the variable if you need to check if a cards type is CustomCardType, do not hardcode the number!
	}

.. code-block:: json
	:linenos:

	{
		"id": "examplemod_custom_card",
		"nameOverride": "Custom Card",
		"descriptionOverride": "a custom card with a custom type!",
		"type": "CustomCardType"
	}
