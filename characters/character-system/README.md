# Character System

The character system is a way to easily manage entities in your game and attach them to Players. The bare bones system allows you to spawn characters on server and clients and connect to state events. It can also be used alongside other systems such as the [Movement System](../character-movement-system/), the Inventory System, and the Damage System.

Use the system in TS with `Airship.Characters`

```typescript
//Set the default prefab to use when spawning a character
Airship.Characters.SetDefaultCharacterPrefab(myCharacter);

//Listen to every new character spawn
Airship.Characters.ObserveCharacters((newCharacter) => {
    //Let the server and client sync
    newCharacter.WaitForInit();
    //Print their display name to the console
    print("Character Spawned: " + newCharacter.GetDisplayName());
})
```
