# Buff
## Description
An instance class which inherits from IBuff, which can serve as an alternative to making a new class for each buff.

## Usage
* Create a new buff that prints to the log when enabled, prints the enemy's position to the log every active frame, and kills the enemy when disabled.
```cs linenums="1"
using ULTRAKIT.Extensions.Classes;
using ULTRAKIT.Loader.Loaders;

public static class BuffCreator
{
	public static void Enable()
	{
		Debug.Log("Buff enabled!");
	}

	public static void Disable()
	{
      	buff.eid.Death();
	}

	public static void OnUpdate()
	{
      	Vector3 pos = buff.eid.transform.position;
      	Debug.Log(pos);
	}

	public static void CreateBuff()
	{
      	Buff buff = new Buff
      	{
      		id = "example.buff",
      		EnableScript = Enable,
      		DisableScript = Disable,
      		UpdateScript = OnUpdate,
      	};
		BuffLoader.RegisterBuff(buff);
	}
}
```
## Properties

| Property      | Type            | Description                                                    |
| ------------- | --------------- | -------------------------------------------------------------- |
| EnableScript  | Action          | Function to be called when the buff is enabled.                |
| DisableScript | Action          | Function to be called when the buff is disabled.               |
| UpdateScript  | Action          | Function to be called every frame the buff is active.          |
| IsActive      | bool            | Whether or not the buff is currently active.                   |
| id            | string          | The unique identifier of the buff.                             |
| eid           | EnemyIdentifier | The EnemyIdentifier of the enemy this instance is attached to. |

# Additional Information
Alternatively, it is possible (and perhaps preferable) to inherit directly from the IBuff interface. After doing so, it must be registered.

## Usage
* Create a new buff that prints to the log when enabled, prints the enemy's position to the log every active frame, and kills the enemy when disabled.
```cs linenums="1"
using ULTRAKIT.Extensions.Interfaces;

public class ExampleBuff : IBuff
{
      public EnemyIdentifier eid { get => _eid; set => _eid = value; }
      public bool IsActive { get => active; }
      public string id => "example.buff";

      private bool active = false;
      private EnemyIdentifier _eid;

      public void Enable()
      {
          active = true;
          Debug.Log("Buff enabled!");
      }

      public void Disable() 
      {
          active = false;
          _eid.Death();
      }

      public void Update() 
      {
          Vector3 pos = _eid.transform.position;
          Debug.Log(pos);
      }
}
```

* An example of registering a buff:
```cs linenums="1"
using ULTRAKIT.Extensions.Interfaces;
using ULTRAKIT.Loader.Loaders;

public static class BuffLoader
{
	public static void RegisterBuffs()
	{
		BuffLoader.RegisterBuff(new ExampleBuff());
	}
}
```

## Properties

| Property      | Type            | Description                                                    |
| ------------- | --------------- | -------------------------------------------------------------- |
| IsActive      | bool            | Whether or not the buff is currently active.                   |
| id            | string          | The unique identifier of the buff.                             |
| eid           | EnemyIdentifier | The EnemyIdentifier of the enemy this instance is attached to. |

## Methods

| Method    | Type | Description                               |
| --------- | ---- | ----------------------------------------- |
| Enable()  | void | Called when the buff is enabled.       |
| Disable() | void | Called when the buff is disabled.      |
| Update()  | void | Called every frame the buff is active. |

