# Creating Accessories

Accessories are stored as prefabs with the AccessoryComponent attached to the root gameObject. You can preview the item using our Accessory Editor

### Create A New Accessory

Any prefab with an AccessoryComponent on its root game object can be used as an accessory.

* Create an empty game object and name it
* Add a component -> AccessoryComponent to the game object
* Select the Slot this accessory will go on
  * If the mesh is skinned to the character select skinned
  * If you want to hide body parts use the Hide Body Parts dropdown
* Drag your mesh(s) onto your game object so they are child transforms
  * If you are bringing in character skinned meshes be sure to delete the bone game objects. The bones will be assigned at runtime to the actual character
  * You can create as many child objects as you want. Including particle effects, primitives or sounds if you want
* Drag your game object into your project to create a prefab of it

<figure><img src="../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

### Accessory Editor

To view your accessory on the character you can click the Accessory Editor button on the AccessoryComponent or go to `Airship -> Avatar -> Accessory Editor`

* Open the accessory editor
* Make sure your item is selected in the Accessory Editor window
* Modify your accessory to look correct on the character
  * You can modify the transform of the root game object, or any child transforms
* Click save to keep your changes or reset to revert back to its last state

{% hint style="info" %}
Hide Body Parts only effects characters at runtime. You will not see the effect in the Accessory Editor
{% endhint %}

### Troubleshooting

* My accessory mesh is invisible in the prefab
  * If it is a character skinned object you must delete the rig transforms which will result in an invisible mesh. However you should see it look correct in the Accessory Editor and in Game
* I don't see my accessory in the Accessory Editor
  * Make sure your accessory is selected in the Accessory Editor window
  * Make sure your transforms positions aren't set way in the distance
  * Make sure you don't have any 0's in your transform scales
  * Make sure you selected the correct slot on your AccessoryComponent
