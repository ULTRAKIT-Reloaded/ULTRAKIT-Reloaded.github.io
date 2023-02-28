# Cheat

Cheat is an instance class that inherits from ICheat, which you can use as an alternative to making a new class for each cheat. It also stores the current active Cheat instance.

To create a new cheat, initialize it and set its values as follows:

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

		CheatsManager.instance.RegisterCheat(cheat, "Example Mod");
	}
}
```

Alternatively, to inherit directly from the ICheat interface, do this instead.

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

Then, in a separate loader class, register it by doing the following:

```cs linenums="1"
public static class CheatsLoader
{
	public static void RegisterCheats()
	{
		CheatsManager.instance.RegisterCheat(new ExampleCheat(), "Example Mod");
	}
}
```