# Player System

Players are the connected users of your game. You have access to a Player object for every connection in the current server. Players can be connect to a spawned character but always exist regardless.

Access this API with `Airship.Players`

```typescript
//Get Local Player
const myLocalPlayer = Game.localPlayer;

//Listen to players that aren't your local player
const nonLocalPlayers: Player[] = [];
Airship.Players.ObservePlayers((newPlayer) => { 
    if(!newPlayer.IsLocalPlayer()){
        nonLocalPlayers.push(newPlayer);
    }
});

//Get a players username from their spawned character
Airship.Characters.ObserveCharacters((character) => {
    //Let the server and client sync their data
    character.WaitForInit();
    print("New character username: " + character.player?.username);
});

//Loop through all players and access their characters
for(const player of Airship.Players.GetPlayers()) {
    const character = player.character;
    if(character) {
        //This player has a spawned character
        ...
    }
}
```
