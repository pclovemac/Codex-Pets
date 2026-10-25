# Astra Chibi look mechanics

The natural gaze motion is led by the blue-gray eyes and eyelids, followed by a restrained head/neck turn and a very small upper-torso follow-through. The feet, lower body, baseline and overall scale remain anchored. The crystal crown stays rigidly attached to the skull; long silver hair follows the head with a small continuous lag. The two-handed clipboard stays attached at chest height and yaws only slightly with the torso, never teleporting or flipping sides.

## Cardinal pose families

- `000 up`: pupils and whole eye surfaces rotate upward; upper lids lift slightly; chin raises a little; crown and bangs follow the head; torso and clipboard remain nearly front-facing.
- `090 screen-right`: nose tip and pupils move to the viewer's right of head center; the face turns right enough to reveal more of the character's left cheek and obscure a little of the right cheek; right-side hair compresses while left-side hair opens; clipboard follows a few degrees right.
- `180 down`: pupils and whole eye surfaces rotate down; upper lids lower; chin dips toward the clipboard; bangs overlap the brow slightly; shoulders relax without shrinking the figure.
- `270 screen-left`: nose tip and pupils move to the viewer's left of head center; the face turns left enough to reveal more of the character's right cheek and obscure a little of the left cheek; left-side hair compresses while right-side hair opens; clipboard follows a few degrees left.

Each 22.5-degree step uses an even combination of eye direction, eyelid/eyebrow change, head yaw/pitch and very small torso/clipboard follow-through. Facial proportions, crown, hair volume and body registration must remain stable; no whole-sprite rotation, skull warp, pupil-only sliding, or independent prop movement.
