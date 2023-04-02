# Render Fixer (Monobehaviour)
## Description
When placed on an object loaded from an asset bundle, it will set all child renderer layers and refresh the applied shaders, which can fix rendering issues.

## Usage
```cs linenums="1"
gameObject.AddComponent<RenderFixer>().Layer = LayerNumber;
```