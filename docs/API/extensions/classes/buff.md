# Buff
Buffis an instance class that inherits from IBuff, which you can use as an alternative to making a new class for each buff.

To create a new buff, initialize it and set its values as follows:

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

Alternatively, to inherit directly from the IBuff interface, do this instead.

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

Then, in a separate loader class, register it by doing the following:

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
