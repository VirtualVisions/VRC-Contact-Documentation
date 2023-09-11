# VRC-Contact-Documentation
The documentation for the up-to-date VRC-Contact audio system.

---
# Base Tools

### Contact Audio Player
This is the main Audio Pool that is used by all Contact components. One of these must exist in the scene for them to function.

| Variables | Description |
| ----------- | ----------- |
| Audio Prefab | The prefab used for spawning audio sources when called. |
| Source Count | The maximum amount of audio sources that will be spawned and pooled. |

### Contact Collision Object
This script is used to give a non-kinematic rigidbody collision sounds. It allows for three tiers of presets: Light, Medium, and Heavy collision type presets.

**NOTE:** If the rigidbody is synced using VRChat's ObjectSync component, then for remote players, it will be treated as "Kinematic" and will not play any collision sounds for players who are not the owner of that object.

| Variables | Description |
| ----------- | ----------- |
| Presets | Light, Medium, and Heavy Presets |
| Max Distance | The maximum distance at which this collision sound can be heard. |

### Contact Footsteps
This is the all-in-one footsteps system, using an array of Presets to declare which sounds go with which object materials.

| Variables | Description |
| ----------- | ----------- |
| Ground Layers | Which layers the system should be looking for collisions, then looking for either materials or a **Contact Footstep Override** |
| Min Landing Velocity | The vertical velocity the player must be falling at in order to play the "Landing" sound effect of a preset. |
| Footstep Rate | Curve determining how much time in seconds (y) should pass between footsteps when the player is going a specific velocity (x). |
| Volume Curve | Curve determining how loud a footstep sound should be played (y) based on how fast the player's velocity is (x). |
| Use Fallback Preset | If enabled, the footstep system will use the first Footstep Preset in the **Presets** array when no preset can be determined otherwise. If disabled, footsteps will continue to use the most recently selected Preset. |
| Presets | The array of **Footstep Presets** used to play audio clips based on materials the player is walking over. |


---
# Presets

### Physics Preset
These presets are used for Contact Collision Objects. These store data that the objects reference and store at build time, letting it be used in VRChat.

| Variables | Description |
| ----------- | ----------- |
| Volume Range | Min and Max values for the randomly selected volume of the played Clips. |
| Pitch Range | Min and Max values for the randomly selected pitch of the played Clips. |
| Minimum Velocity | The velocity the object must be travelling at before these Clips will be used. |
| Clips | The audio clips associated with this Preset. |


### Surface Preset
This is the base form of the Footstep Presets. This is largely included as a way to expand on your own systems with your own presets, such as the included **Gun** demo.

| Variables | Description |
| ----------- | ----------- |
| Materials | Which materials to associate with this preset. |
| Clips | Which audio clips to be used with this preset. |


### Footstep Preset
These are the presets used by the Contact Footstep system, and includes all variables in Surface Preset, as well as those listed here.

| Variables | Description |
| ----------- | ----------- |
| Jump Clips | Audio clips used when the player jumps off of this surface. |
| Landing Clips | Audio clips used when the player lands onto this surface. |

---
# Demo Tools

### Contact Gunshots
This demo plays an audio clip at the position shot via the player using a VRCPickup. This clip changes depending on the material hit. Since no gunshot audio clips are included, the demo just uses the footstep sounds.

| Variables | Description |
| ----------- | ----------- |
| Presets | The Surface or Footstep presets used for the gunshot presets. |
| Fire Point | The transform at which the pickup fires it's raycast from. |
| Hit Layers | The layers that the gun is able to hit. |


### ContactDemo Play Sound At Point
This script is used for button objects, acting as the main demo for understanding how to interface with the **Contact Manager**.

| Variables | Description |
| ----------- | ----------- |
| Clip | The audio clip intended to be played. |
| Point | The transform reference for where the clip will be played. If none is provided, the clip will be played at the root of the object this script is on. |
| Volume | A value from 0 to 1 for how loud the sound will be. |
| Parent Clip | Whether or not to parent the spawned audio source to the Point reference. |
| Cut Off Previous | Whether or not to interrupt an already playing sound to allow this sound to play. |
| Max Distance | The distance at which this clip will reach from the Point. |

### ContactDemo Reset Objects
A simple respawner for non-synced objects, letting the player observe the interactions of the Contact Collision Objects repeatedly.

| Variables | Description |
| ----------- | ----------- |
| Props | All rigidbodies intended to be reset by this button. |
