.. include:: ../global.rst

Awake or Ready?
###############

The ``Mod`` class has 2 methods which are called during different parts of the game loading process:
``Awake`` and ``Ready``.

**When to use Awake?**

Awake is called before any game data is loaded. This is the part where you should create your harmony
patches, extend enums, and more. ``ModManager`` is the only available manager at this time, so trying
to access other manager classes will result in errors.

**When to use Ready?**

Ready is called after all game data is loaded. If you want to modify the data of ``WorldManager.CardDataPrefabs``
for example, this is when you should do it.

:raw-html:`<hr>`

#. ``Awake()``
#. Game data gets loaded
#. ``Ready()``