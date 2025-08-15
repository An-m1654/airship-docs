# Resources Folder

In Unity, any folder name `Resources` will be setup its files to be loaded at runtime via local paths.&#x20;

To load these assets in Airship use the `Asset` class:

```typescript
const myPrefab: GameObject =  Asset.LoadAsset("Local/Path/From/Resources.prefab");
```

{% hint style="info" %}
Look to the Unity [Resources Folder](https://docs.unity3d.com/ScriptReference/Resources.html) page for more information.
{% endhint %}
