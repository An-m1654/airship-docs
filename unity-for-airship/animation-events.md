---
description: >-
  Create and capture animation events to run functions in code when your
  animation hits a specific location.
---

# Animation Events

## Overview

In Airship animation events are passed to Typescript through the AnimationEventListener component. If you add this component to your animator it will pass along events from your animations. Airship Characters have this component by default.

{% hint style="info" %}
Naming is important here. All animation events must fire the function "TriggerEvent" to be passed into Typescript.&#x20;
{% endhint %}

## Create Animation Events

To setup an event use Unity's animation event system either in the animation clip itself using the animation window, or on an FBX using the inspector window.&#x20;

1. Create a new animation event
2. Give it the function `TriggerEvent`
3. Set the triggers key to be whatever you would like to identify it by

<figure><img src="../.gitbook/assets/image (19).png" alt="" width="344"><figcaption><p>MyAnimationEvent On Animation Clip</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (110).png" alt="" width="355"><figcaption><p>MyAnimationEvent On FBX Animation</p></figcaption></figure>



## Listening To Animation Events

To listen to events in Typescript, get the component reference for the AnimationEventListener, then connect to the OnAnimationEvent Signal on Character.animator:

```typescript
//Get the component (or you can setup a reference if in an AirshipBehaviour)
const events = this.gameObject.GetComponent<AnimationEventListener>();
if(events){
	//Connect to simple events
	events.OnAnimEvent((key)=>{
		//Key is the string value you specify in editor
		if(key === "MyAnimationEvent"){
			///Do Stuff
			print("Heard my event!");
		}
	})
}
```

{% hint style="info" %}
Characters by default have an AnimationEventListener and can be listened to through a signal on Character.animation.OnAnimationEvent which is more performant than directly accessing the characters AnimationEventListener.

Read more on the [Character Animations Page](../characters/character-animations/)
{% endhint %}

### Optional - Pass Data With Event

If you need additional data passed along with the event, you can include an AnimationEventData scriptable object.

1. In your project, right click to `Create -> Airship -> Animation Event Data`
   1. Fill in the objects data with whatever you want to receive in TS
2. On your animation, Set the event function to `TriggerEventObj`&#x20;
3. Set the Object variable to the Animation Event Object you created

<figure><img src="../.gitbook/assets/image (112).png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

Now to receive this event in Typescript

```typescript
//Get the component (or you can setup a reference if in an AirshipBehaviour)
const events = this.gameObject.GetComponent<AnimationEventListener>();
if(events){
	//Connect to object event
	events.OnAnimObjEvent((data)=>{
		//key is used to identify the event
		if(data.key === "MyAnimationEventObj"){
			///Do Stuff with the extra data
			print("New Float: " + data.floatValue);
		}
	})
}
```

