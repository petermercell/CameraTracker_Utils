# CameraTracker Utils

A collection of TCL scripts for Nuke that extend and streamline CameraTracker workflows — converting 3D data to 2D tracks, connecting locators, and assisting with difficult tracking scenarios.

## Tools

### Locators2Tracker_PM.tcl
Converts 3D Locator/Axis positions from a CameraTracker solve into 2D tracker data. Automates the tedious process of manually setting up Reconcile3D nodes for each point — select your locators and generate a Tracker node with all the 2D tracks in one step.

**Use cases:**
- Creating 2D tracks from CameraTracker point cloud for roto
- Generating corner pins from 3D reference points
- Exporting 2D tracking data for other applications

### AxisConnect_PM.tcl
Connects Axis nodes to CameraTracker points, streamlining the process of creating positioned 3D elements at tracked locations in your scene.

**Use cases:**
- Placing 3D geometry at specific tracked points
- Creating reference locators from point cloud data
- Building projection setups from CameraTracker solves

### TrackAssist_PM.tcl
Uses CameraTracker data to guide 2D tracking in areas where the standard Tracker node struggles. Generates relative motion from the camera solve to assist tracking points in challenging regions like motion blur, low contrast, or occluded areas.

**Use cases:**
- Tracking features in difficult areas using 3D motion as reference
- Recovering failed 2D tracks with camera solve guidance
- Improving tracking accuracy with triangulation

### AxisToRender.tcl
Sets up Axis nodes for rendering, creating the necessary connections for outputting positioned elements through the 3D system by Gaetan Baldy.

## Installation

1. Copy the `.tcl` files to your `.nuke` directory
2. Add to your `menu.py`:
   ```python
   import nuke
   
   toolbar = nuke.menu('Nodes')
   m = toolbar.addMenu('CameraTracker Utils')
   m.addCommand('Locators2Tracker', 'nuke.load("Locators2Tracker_PM"); Locators2Tracker_PM()')
   m.addCommand('AxisConnect', 'nuke.load("AxisConnect_PM_v003"); AxisConnect_PM()')
   m.addCommand('TrackAssist', 'nuke.load("TrackAssist_PM"); TrackAssist_PM()')
   m.addCommand('AxisToRender', 'nuke.load("AxisToRender"); AxisToRender()')
   ```

Or source them directly in Nuke's Script Editor when needed.

## Requirements

- Nuke (with CameraTracker — NukeX or Nuke Studio)
- Solved CameraTracker with point cloud data

## Workflow

These tools are designed to work with CameraTracker solves:

1. **Track** your footage with CameraTracker and solve the camera
2. **Create Scene** to generate the point cloud and camera
3. Use **AxisConnect** to place Axis nodes at tracked points
4. Use **Locators2Tracker** to convert those 3D positions to 2D tracks
5. Use **TrackAssist** if you need to track additional features in difficult areas

## Author

[Peter Mercell](https://github.com/petermercell)
