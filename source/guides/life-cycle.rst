Mod Life-cycle
##############

This page documents the life-cycle of a Mod class, as well as other relevant GameObjects.

#. The SceneBootstrapper instantiates the board prefabs and the manager GameObjects.
#. After the most essential managers are created (SteamManager, SaveManager, etc.) the ModManager is created
#. ModManager looks for mod folders (specifically, ``manifest.json`` files) in the local Mods folder [1]_ and Steam Workshop folders
#. The assemblies are loaded, and each found Mod class (one per assembly!) is added as a component to the ModManager (if a Mod class is not found or the assembly is missing, a default Mod class is created), and fields such as ``Harmony`` and ``Logger`` are initalized so they are accessible in the mods Awake method
#. The GameDataLoader loads all vanilla content, then loads the modded cards, blueprints, and packs
#. After all vanilla content has been loaded, ``localization.tsv`` files get loaded from the mod folders, and the ``Ready`` method is invoked on each Mod class

.. [1] Windows: ``%userprofile%\AppData\LocalLow\sokpop\Stacklands\Mods`` | Mac: ``~/Library/Application Support/sokpop/Stacklands/Mods`` (or ``~/Library/Application Support/com.sokpop.Stacklands/Mods``, Unity is a mess)