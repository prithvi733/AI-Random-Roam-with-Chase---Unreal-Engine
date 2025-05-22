# AI-Random-Roam-with-Chase---Unreal-Engine
# 🎯 Aim:
To create an AI character in Unreal Engine that roams randomly within a NavMesh area and chases the player when they come within a certain range, using Behavior Trees, Blackboard, and AI Perception.

# 🛠 Procedure:
1.Setup Navigation
.Add a NavMeshBoundsVolume to your level and scale it to cover the roamable area.
.Press P to confirm the green nav area is visible (indicating navigable space).

2.Create AI Character
.Create a Blueprint character (e.g., BP_AIEnemy) with a skeletal mesh and AIController class.
.Create an AI Controller Blueprint (e.g., BP_AIController) and assign it to the character.

3.Enable AI Perception
.In BP_AIController, add an AIPerception component.
.Configure a Sight sense (set detection range, lose sight range, peripheral vision angle).
.Bind OnPerceptionUpdated to update a blackboard value (e.g., CanSeePlayer and PlayerActor).

4.Set Up Blackboard
.Create a Blackboard with the following keys:
.TargetLocation (Vector)
.PlayerActor (Object)
.CanSeePlayer (Bool)

5.Create Behavior Tree (BT_AI)
.Structure it like this:

.Root └── Selector ├── Sequence (Chase Player) │ ├── Blackboard Check: CanSeePlayer == true │ └── Move To: PlayerActor └── Sequence (Random Roam) ├── Task: Find Random Location → TargetLocation └── Move To: TargetLocation

6.Custom Task: Find Random Location
.Create a new BTTask_BlueprintBase to get a random reachable point using: cpp UNavigationSystemV1::GetRandomReachablePointInRadius()
.Set the result to the TargetLocation blackboard key.

7.Test the AI
.Add a player character to the level.
.Place the AI enemy in the map and assign its controller and behavior tree.
.Press Play: the AI should roam when the player is far and chase the player when within sight.

# Output:
![image](https://github.com/user-attachments/assets/75f8d31a-9307-4316-a6bd-58cd70096c86)

![image](https://github.com/user-attachments/assets/25e9d7d9-2926-4cb4-ad3f-d9d1ea69b3a5)

![image](https://github.com/user-attachments/assets/8c1e8581-e33f-4775-b393-e3e555337a7c)

# ✅ Result:
The AI character roams randomly within a defined area. When the player enters its sight range, the AI stops roaming and begins to chase the player until the player is out of sight, after which it resumes roaming.


