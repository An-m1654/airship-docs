# Character Movement Physics

## The Physics Setup

The character is controlled by a Rigidbody and Box Collider. The Box Collider is axis aligned. Meaning the root of your character DOES NOT ROTATE.&#x20;

The rotation happens purely on the graphical elements of the hierarchy. Specifically on the NetworkedGraphicsHolder. So if you want to get the rotation of the character you will need to grab the rotation from that transform, or use the look vector from the CharacterMovement component

```typescript
//To get the characters rotation
character.movement.graphicTransform.rotation;

//To get the look vector of the character
character.movement.GetLookVector();
```

The rigibodies forces are controlled by the CharacterMovement component. If you want to add forces you can use the Impulse functions. If you want to control the velocity you can use the SetVelocity function.

```typescript
//Add an instant force to the characters rigidbody
character.movement.AddImpulse(Vector3.forward.mul(10));

//Stop all motion
character.movement.SetVelocity(Vector3.zero);
```

Its easy to check if another component has collided with the characters. Simply check for the Character component, or any other component on the root of the Character prefab.&#x20;

```typescript
import Character from "@Easy/Core/Shared/Character/Character";

export default class KnockbackCollider extends AirshipBehaviour {
    public knockbackForce: Vector3;

    protected OnTriggerEnter(collider: Collider): void {
        let character = collider.attachedRigidbody?.gameObject.GetAirshipComponent<Character>();
        if(character){
            //Interact with character
            character.movement.AddImpulse(this.knockbackForce);
        }
    }
}
```
