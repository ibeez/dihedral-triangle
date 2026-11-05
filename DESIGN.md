---
type: design
---
# Fig. 14 · The Dihedral Group (design)

For the builder. Tactile ASCII exploration of the Dihedral Group D_3 (symmetries of an equilateral triangle).

## Intent
Fig. 14 in Judy's "math facts that live in my head" series.
The math fact: D_3, order changes the destination. Symmetries of an equilateral triangle.
The moment: Turn then Flip lands in a completely different posture than Flip then Turn (r · f ≠ f · r). Changing the order of actions changes where you end up.

## The Math Truth
- Group: D_3, the dihedral group of degree 3 (order 6). It is isomorphic to S_3, the symmetric group on 3 elements.
- Vertices: [1], [2], [3] at the three corners of an equilateral triangle.
- Standard posture (e, identity):
  - Top vertex: [1]
  - Bottom-right vertex: [2]
  - Bottom-left vertex: [3]
  - Face orientation: Up (cool faint indigo)
- Two fundamental verbs:
  - Turn (r): 120 degree clockwise rotation.
  - Flip (f): horizontal reflection across the vertical axis through the apex.
- The 6 group elements:
  - 3 Rotations (Face Up):
    - e: identity (0 degree turn) -> corners [1, 2, 3]
    - r: one turn clockwise (120 degrees) -> corners [3, 1, 2]
    - r^2: two turns clockwise (240 degrees) -> corners [2, 3, 1]
  - 3 Reflections (Face Down):
    - f: flip from identity -> corners [1, 3, 2]
    - rf: turn then flip -> corners [3, 2, 1]
    - r^2f: two turns then flip (equal to flip then turn) -> corners [2, 1, 3]
- Subgroups:
  - Rotational subgroup: <r> = {e, r, r^2}, cyclic subgroup of order 3.
  - Reflection subgroups: <f> = {e, f}, <rf> = {e, rf}, <r^2f> = {e, r^2f}, each of order 2.
- The Core Reveal (Non-commutativity):
  - Start at e:
    - Path A (Turn then Flip): r · f = rf. Corner [3] is at top, face is down.
    - Path B (Flip then Turn): f · r = r^2f. Corner [2] is at top, face is down.
  - Since rf ≠ r^2f, the operations do not commute.
  - In algebraic terms: f · r · f = r^-1 = r^2, which gives r · f = f · r^2.

## ASCII Architecture and Visual Layout
- Plate size: 1200 x 1000 pixels.
- Background: warm paper (#f4eee6) with subtle seamless organic fiber texture.
- Frame: single thin brass rule with hand-set corner joints (Blue Grey B47).
- Split layout:
  1. The Physical Triangle (Left, centered at x = 390, y = 525):
     - Equilateral triangle with radius 195 px.
     - Lettered corners [1], [2], [3] rendered in Gaegu 700 with clear position tracking.
     - Edges rendered with tight lowercase words ("turn " and "flip ") on a 12.5 px grid.
     - Turn: smooth 120 degree clockwise rotation.
     - Flip: 3D horizontal squash (scaleX 1 -> 0 -> -1).
     - Face colors:
       - Face up: cool faint indigo fill (#0846a9 at 5% opacity).
       - Face down: warm cantaloupe fill (#ffc137 at 18% opacity).
  2. The 6-State Cayley Map (Right, centered at x = 880, y = 525):
     - Two concentric 3-node rings:
       - Outer ring (radius 195 px): 3 face-up states (e, r, r^2).
       - Inner ring (radius 110 px): 3 face-down states (f, rf, r^2f).
     - Directed circular arcs for Turn:
       - Outer ring turns clockwise: e -> r -> r^2 -> e.
       - Inner ring turns counter-clockwise: f -> r^2f -> rf -> f.
     - Radial straight bridges for Flip:
       - e <-> f
       - r <-> rf
       - r^2 <-> r^2f
     - Active node lights up bold Warm Coral (Warm Coral 208) with Gaegu 700.
     - Inactive nodes rest in cool faint POSCA Indigo.
  3. Interactive Controls (Bottom row, y = 872):
     - Plain word buttons: [ Turn ] [ Flip ] [ Does order matter? ] [ Reset ].
     - Keyboard shortcuts: T for turn, F for flip, Space for showdown, 0 or R for reset.

## The Showdown: Does Order Matter?
- Animates Path A:
  - Turn then Flip.
  - Traces a blue path on the Cayley map from e to r, then r to rf.
  - Triangle lands on posture [3, 2, 1] (face down).
- Animates Path B:
  - Flip then Turn.
  - Traces a coral path on the Cayley map from e to f, then f to r^2f.
  - Triangle lands on posture [2, 1, 3] (face down).
- The map shows both trails landing on opposite sides of the inner ring.
- Caption: "order changes the destination".
- Equation: "r · f ≠ f · r  (rf ≠ r²f)".

## The 16 s Loop (Autoplay Reel)
480 frames at 30 fps, 120 BPM:
- 0.0 s to 3.6 s: 3 Turns.
  Hops e -> r -> r^2 -> e.
  Triangle rotates 360 degrees.
  Caption: "3 turns bring you home (order 3)".
  Math: "r · r · r = e".
- 3.6 s to 6.8 s: 2 Flips.
  Flips e -> f -> e.
  Triangle flips face-down then face-up.
  Caption: "2 flips bring you home (order 2)".
  Math: "f · f = e".
- 6.8 s to 15.0 s: The Order Showdown.
  - 7.0 s: Path A begins. Turn then Flip (e -> r -> rf). Blue trail traces map.
  - 9.4 s: Reset to e.
  - 10.0 s: Path B begins. Flip then Turn (e -> f -> r^2f). Coral trail traces map.
  - 12.0 s: Both endpoints highlighted.
  - Caption: "order changes the destination".
  - Math: "r · f ≠ f · r  (rf ≠ r²f)".
- 15.0 s to 16.0 s: Trails fade, state relaxes cleanly to e, loop closes at frame 0.

## Audio Design
Synthesized in Web Audio API:
- Key: D minor / F major modal pentatonic.
- Notes per state:
  - State e (identity): F4 (349.2 Hz)
  - State r (turn 1): A4 (440.0 Hz)
  - State r^2 (turn 2): C5 (523.3 Hz)
  - State f (flip): D4 (293.7 Hz)
  - State rf (turn then flip): G4 (392.0 Hz)
  - State r^2f (flip then turn): Bb4 (466.2 Hz)
- Sound effects:
  - Turn action: ascending wooden rototap and tuned chime.
  - Flip action: resonant wooden slap and warm dual gong.
  - Showdown contrast: split chime ringing on rf and r^2f to emphasize divergence.
  - Button tap: crisp wooden tick.
- Ambient rhythm: soft music box pattern at 120 BPM with celesta lead.
