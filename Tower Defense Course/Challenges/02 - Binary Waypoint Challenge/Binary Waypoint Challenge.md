Before starting this challenge, you should complete [[07 - Waypoints]].

In this challenge, you are tasked with creating a **Binary Waypoint** that can connected up to **TWO** other **Binary Waypoints**.
## Import Challenge

- [ ] Download the Binary Waypoint Challenge: [[BinaryWaypointChallenge V1.0.0.unitypackage]]
- [ ] Import the package into your Unity Project

## Tasks
- [ ] Open the Binary Waypoint Challenge
- [ ] Create a **Binary Waypoint** Prefab
- [ ] The **Binary Waypoint** Prefab should have 3D Cube
- [ ] Create a **BinaryWaypoint** MonoBehaviour Script
	- [ ] Create a **First** Property that is a **BinaryWaypoint**
	- [ ] Create a **Second** Property that is a **BinaryWaypoint**
	- [ ] Both properties should be visible in the inspector
- [ ] Implement the **OnDrawGizmos** method
	- [ ] Draw a red line from the waypoint to **First**
	- [ ] Draw a yellow line from the waypoint to **Second**
	- [ ] Add null checks such that 0, 1, or 2, waypoints can be specified
- [ ] Add **Binary Waypoints** to the scene to match the image below

![[binary-waypoint-connections.png]]

- [ ] Ensure that the **Binary Waypoints** are not visible in the **Game View**

![[no-waypoints-visible.png]]