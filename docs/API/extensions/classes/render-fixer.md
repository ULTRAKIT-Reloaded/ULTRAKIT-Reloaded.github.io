# Render Fixer (Monobehaviour)

When placed on an object loaded from an asset bundle, it will fix the object rendering on the layer specified.

Properly adding the render fixer is done as follows:

```cs linenums="1"
gameObject.AddComponent<RenderFixer>().Layer = LayerNumber;
```