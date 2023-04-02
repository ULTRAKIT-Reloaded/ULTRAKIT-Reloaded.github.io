# Cheat
## Description
An instance class which inherits from ICheat, which can serve as an alternative to making a new class for each cheat. It also stores the current active Cheat instance.

## Usage
* Create a new cheat that prints to the log when enabled, disabled, and active frame.
```cs linenums="1"
using ULTRAKIT.Extensions.Classes;

public static class CheatCreator
{
	public static void OnEnable()
	{
		Debug.Log("Cheat enabled!");
	}

	public static void OnDisable()
	{
		Debug.Log("Cheat disabled!");
	}

	public static void OnUpdate()
	{
		Debug.Log("Cheat is currently active!");
	}

	public static void CreateCheat()
	{
		Cheat cheat = new Cheat()
		{
			LongName = "Example Cheat",
			Identifier = "example.cheat",
			ButtonEnabledOverride = "Cheat Active",
			ButtonDisabledOverride = "Cheat Inactive",
			DefaultState = false,
			PersistenceMode = StatePersistenceMode.NotPersistent,
			EnableScript = OnEnable,
			DisableScript = OnDisable,
			UpdateScript = OnUpdate
		};

		// Registers a cheat to the specified category
		CheatsManager.instance.RegisterCheat(cheat, "Example Mod");
	}
}
```
## Properties

| Property               | Type                 | Description                                                                                     |
| ---------------------- | -------------------- | ----------------------------------------------------------------------------------------------- |
| EnableScript           | Action               | Function to be called when the cheat is enabled.                                                |
| DisableScript          | Action               | Function to be called when the cheat is disabled.                                               |
| UpdateScript           | Action               | Function to be called every frame the cheat is active.                                          |
| Instance               | Cheat                | The current active cheat instance.                                                              |
| IsActive               | bool                 | Whether or not the cheat is currently active.                                                   |
| LongName               | string               | The display name of the cheat.                                                                  |
| Identifier             | string               | The unique identifier of the cheat.                                                             |
| ButtonEnabledOverride  | string               | The text displayed on the cheat button when enabled.                                            |
| ButtonDisabledOverride | string               | The text displayed on the cheat button when disabled.                                           |
| DefaultState           | bool                 | The default state of the cheat when cheats are enabled.                                         |
| PersistenceMode        | StatePersistenceMode | Whether the cheat should stay enabled/disabled after reload when Keep Cheats Enabled is active. |
| Icon                   | string               | The key of an icon in the private `CheatsManager.Instance.spriteIcons` dictionary. This is locked to "warning".        |

# Additional Information
Alternatively, it is possible (and perhaps preferable) to inherit directly from the ICheat interface. After doing so, it must be registered.

## Usage
* Create a new cheat that prints to the log when enabled, disabled, and every active frame.
```cs linenums="1"
public class ExampleCheat : ICheat
{
	public string LongName => "Example Cheat";
	public string Identifier => "example.cheat";
	public string ButtonEnabledOverride => "Cheat Active";
	public string ButtonDisabledOverride => "Cheat Inactive";
	public bool DefaultState => false;
	public bool IsActive => false;
	public string Icon => "warning";
	public StatePersistenceMode PersistenceMode => StatePersistenceMode.NotPersistent;

	public void Enable()
	{
		Debug.Log("Cheat enabled!");
	}

	public void Disable()
	{
		Debug.Log("Cheat disabled!");
	}

      public void Update()
	{
		Debug.Log("Cheat is currently active!");
	}
}
```

* An example of registering a cheat
```cs linenums="1"
public static class CheatsLoader
{
	public static void RegisterCheats()
	{
		// Registers a cheat to the specified category
		CheatsManager.instance.RegisterCheat(new ExampleCheat(), "Example Mod");
	}
}
```

## Properties

| Property               | Type                 | Description                                                                                                                             |
| ---------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| IsActive               | bool                 | Whether or not the cheat is currently active.                                                                                           |
| LongName               | string               | The display name of the cheat.                                                                                                          |
| Identifier             | string               | The unique identifier of the cheat.                                                                                                     |
| ButtonEnabledOverride  | string               | The text displayed on the cheat button when enabled.                                                                                    |
| ButtonDisabledOverride | string               | The text displayed on the cheat button when disabled.                                                                                   |
| DefaultState           | bool                 | The default state of the cheat when cheats are enabled.                                                                                 |
| PersistenceMode        | StatePersistenceMode | Whether the cheat should stay enabled/disabled after reload when Keep Cheats Enabled is active.                                         |
| Icon                   | string               | The key of an icon in the private `CheatsManager.Instance.spriteIcons` dictionary (cloned from the `IconManager.Instance.CurrentIcons.cheatIcons` dictionary). |

## Methods

| Method    | Type | Description                             |
| --------- | ---- | --------------------------------------- |
| Enable()  | void | Called when the cheat is enabled.       |
| Disable() | void | Called when the cheat is disabled.      |
| Update()  | void | Called every frame the cheat is active. |

Valid icons (by default) are:

| Key                   | Standard Icon                                                      | PITR Icon                                                        |
| --------------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------- |
| "grid"                | ![Standard](/../../assets/images/cheats/Grid 1.png)                | ![Standard](/../../assets/images/cheats/Grid.png)                |
| "wall-jumps"          | ![Standard](/../../assets/images/cheats/Infinite Wall Jumps 1.png) | ![Standard](/../../assets/images/cheats/Infinite Wall Jumps.png) |
| "navmesh"             | ![Standard](/../../assets/images/cheats/NavMesh 1.png)             | ![Standard](/../../assets/images/cheats/NavMesh.png)             |
| "no-enemies"          | ![Standard](/../../assets/images/cheats/No Enemy Spawns 1.png)     | ![Standard](/../../assets/images/cheats/No Enemy Spawns.png)     |
| "physics"             | ![Standard](/../../assets/images/cheats/Physics 1.png)             | ![Standard](/../../assets/images/cheats/Physics.png)             |
| "no-weapon-cooldown"  | ![Standard](/../../assets/images/cheats/No Weapon Cooldowns 1.png) | ![Standard](/../../assets/images/cheats/No Weapon Cooldowns.png) |
| "flight"              | ![Standard](/../../assets/images/cheats/Flight 1.png)              | ![Standard](/../../assets/images/cheats/Flight.png)              |
| "noclip"              | ![Standard](/../../assets/images/cheats/Noclip 1.png)              | ![Standard](/../../assets/images/cheats/Noclip.png)              |
| "blind"               | ![Standard](/../../assets/images/cheats/Blind 1.png)               | ![Standard](/../../assets/images/cheats/Blind.png)               |
| "warning"             | ![Standard](/../../assets/images/cheats/Warning 1.png)             | ![Standard](/../../assets/images/cheats/Warning.png)             |
| "spawner-arm"         | ![Standard](/../../assets/images/cheats/Spawner Arm 1.png)         | ![Standard](/../../assets/images/cheats/Spawner Arm.png)         |
| "save"                | ![Standard](/../../assets/images/cheats/Save 1.png)                | ![Standard](/../../assets/images/cheats/Save.png)                |
| "load"                | ![Standard](/../../assets/images/cheats/Quick Load 1.png)          | ![Standard](/../../assets/images/cheats/Load.png)                |
| "delete"              | ![Standard](/../../assets/images/cheats/Delete 1.png)              | ![Standard](/../../assets/images/cheats/Delete.png)              |
| "quick-load"          | ![Standard](/../../assets/images/cheats/Load 1.png)                | ![Standard](/../../assets/images/cheats/Quick Load.png)          |
| "teleport"            | ![Standard](/../../assets/images/cheats/Teleport 1.png)            | ![Standard](/../../assets/images/cheats/Teleport.png)            |
| "infinite-wall-jumps" | ![Standard](/../../assets/images/cheats/Infinite Wall Jumps 1.png) | ![Standard](/../../assets/images/cheats/Infinite Wall Jumps.png) |
| "infinite-power-ups"  | ![Standard](/../../assets/images/cheats/Infinite Power Ups 1.png)  | ![Standard](/../../assets/images/cheats/Infinite Power Ups.png)  |
| "invincible-enemies"  | ![Standard](/../../assets/images/cheats/Invincible Enemies 1.png)  | ![Standard](/../../assets/images/cheats/Invincible Enemies.png)  |
| "light"               | ![Standard](/../../assets/images/cheats/fullbright 1.png)          | ![Standard](/../../assets/images/cheats/fullbright.png)          |
| "clash"               | ![Standard](/../../assets/images/cheats/CrashMode 1.png)           | ![Standard](/../../assets/images/cheats/CrashMode.png)           |
| "death"               | ![Standard](/../../assets/images/cheats/Death 1.png)               | ![Standard](/../../assets/images/cheats/Death.png)               |