Controls:
 E->open the normal Door
 L-Mouse_Grabable door
 F-Toggle on and off flashlight
 L-ctrl crouch
 L-Shift Sprint


Physics-based Door Mechanism Summary
  *Detection: Uses a Line Trace from the Camera's World Location to find the Door Actor within a specific range (350 units).

  *Variable Storage: The detected door is saved as a GrabbedObject variable to keep the connection steady during interaction.

  *Communication: Uses a Blueprint Interface (BPI_Interaction) to send a "Grab" signal from the Player to the Door.

  *Player Control: Upon interaction, the system calls Disable Movement and Ignore Look Input to lock the player in place while they move the door.

  *Physics Setup:

  *Mass: Set to 150kg with Simulate Physics enabled for a realistic weight.

  *Constraint: A Physics Constraint acts as the hinge, locking the door to its frame while allowing specific rotation.

  *Limits: Linear Motion is locked, and Angular Swing is limited (e.g., 50°) to prevent the door from spinning through walls.

  *Direction Logic: Uses a Dot Product calculation (comparing Door Forward vs. Player Position) to determine if the player is in front of or behind the door.

  *Movement: Multiplies the Mouse X axis input by a Select Float (1.0 or -1.0 based on Dot Product) to rotate the door dynamically using Combine Rotators.

**Flashlight (Spotlight) Toggle Mechanism**
  *Input Action: Uses the Enhanced Input System (specifically the IA_Flashlight action) to detect when the player presses the flashlight key.
  
  *Toggle Logic: When the input is Started, it triggers a Branch node to check the current status of the light.
  
  *Visibility Check: The Target is the Spot Light component; the branch checks its current Is Visible state.
  
State Switching:
  
  *If True (Light is on), it calls Set Visibility with the New Visibility checkbox unchecked to turn it off.
  
  *If False (Light is off), it calls Set Visibility with the New Visibility checkbox checked to turn it on.
  
  *Placement Logic: The Spotlight is attached to a Spring Arm with a Target Arm Length of 10 and a Z-axis offset of -30.
  
  *Functional Benefit: This specific placement ensures the light stays steady near the camera (chest level) and doesn't clip through walls during interaction.
  
  **FLicker Light and Player Sprint mechanism Add.** 
