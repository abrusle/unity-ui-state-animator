# Objective

Create a framework that handles animating between multiple given UI states.
Provide the workflow and tools for creating and editing UI states (RectTransform properties, etc.) while allowing a preview of those changes in the scene. The tools should feature a set of customizable properties such as animation curve, duration for each transition.


## Implementation Idea 1

- Have the user define ui states using animation clips (source animation clips). The properties of each state are defined by the keyframes in the first frame of the source clips.
- These clips are then grouped in a ScriptableObject which generates:
    - Animation clips interpolating between the given states
    - An animation controller able to transition between states
- The SO can take parameters to generate the transition animations such as: animationCurves and durations.

### Limitations
- Detecting when the user changes keyframes in the source animation clips.
- Previewing ui states in the scene when editing source animation clips.
    - the user could add an Animation component in the scene and preview the clip directly. This is far from ideal because the animation component might conflict with the Animator (Animation Controller) used for runtime animation
- Allowing animated properties to be dynamically changed via script at runtime (e.g. responsive transfroms)
    - Can be solved by allowing the user to extract the generated asset from the SO and make further changes to them.
- 