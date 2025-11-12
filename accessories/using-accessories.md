---
description: >-
  In code accessories are managed by the AccessoryBuilder. The accessory builder
  places items into slots and runs the MeshCombine to optimize the character
  with its new look.
---

# Using Accessories

### Add / Remove Accessories

To add or remove an item simply call methods on the characters accessoryBuilder.

* To Add an accessory
  * `character.accessoryBuilder.Add(prefabInProject);`
* To Remove an accessory
  * `character.accessoryBuilder.RemoveBySlot(AccessorySlot.Head);`
  * `character.accessoryBuilder.RemoveAll();`
  * `character.accessoryBuilder.RemoveClothingAccessories();`



### Working with Outfits

Often the character will be loading their select outfit which writes to the accessory builder. So if you want overwrite someones outfit you will need to wait for it to load, then modify it.&#x20;

{% hint style="info" %}
If you don't want characters to auto load their outfit, there is an option on the `Character` component of your character prefab.
{% endhint %}

Below is an example of waiting for the outfit load and then adding your own accessories.

```typescript
import { Airship } from "@Easy/Core/Shared/Airship";

export default class LoadAccessoryList extends AirshipBehaviour {
	@Header("Accessory Prefabs")
	@Tooltip("Requires AccessoryComponent")
	public accPrefabs: GameObject[];

	private loadingOurAccessories = false;

	override Start(): void {
		// Listen for the local character
		Airship.Characters.ObserveCharacters((char) => {
			char.WaitForInit();
			if (char.IsLocalCharacter()) {
				// This is the local character
				// Mesh combined fires when new accessories are added to the character
				// So if your character auto loads its outfit this will fire
				char.accessoryBuilder.OnMeshCombined.Connect(() => {
					// Make sure this event isn't from our CombineMesh call
					if (this.loadingOurAccessories) {
						this.loadingOurAccessories = false;
						return;
					}
					this.loadingOurAccessories = true;
					
					// Add each accessory from our prefab list
					for (const acc of this.accPrefabs) {
						char.accessoryBuilder.Add(acc.GetComponent<AccessoryComponent>()!);
					}

					// Regenerate the character mesh with the new accessories
					char.accessoryBuilder.UpdateCombinedMesh();
				});
			}
		});
	}
}

```
