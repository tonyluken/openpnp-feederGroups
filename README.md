# openpnp-feederGroups
Compiled OpenPnP .jar file with feeder groups (based on openpnp PR 943)

# Description
This allows feeders to be grouped together such that they can be moved/rotated and enabled/disabled as a group. At the time of this writing it supports all feeder types except BlindsFeeder and ReferenceSlotAutoFeeder.  The intention of feeder groups is to allow users to remove groups of feeders from their machine and quickly re-align them when the group of feeders is returned to the machine. Aligning the feeder group is accomplished quickly using two fiducial marks and automatically updates the location information of all its descendants.

# WARNING - Backup your machine.xml file before trying this!!!
Copy the .jar file to your computer and run it as you would normally run openpnp.

# Instructions for Use
A Feeder Group needs to have a physical basis. It can be something very simple or some precision milled/3D printed part. The size and shape doesn't matter as long as it provides a means to securely hold the feeders that are physically attached to it. As an example, it could be a simple aluminum sheet about the thickness of a PCB with double-sided tape to hold strip feeders. The physical feeder group also needs two fiducial marks preferably placed as far apart as possible - these can be the same type marks as used for the machine's homing fiducial mark (FIDUCIAL-HOME) or something different as long as it is defined on the Parts tab. One of the fiducial marks should be labeled "A" and the other "B". Follow these detailed instructions to setup a feeder group:

1) Attach the feeders to the physical feeder group and place it on the machine.
2) On the Feeders tab, click the + to add a new feeder and select ReferenceFeederGroup.
3) Optional - double click on its name and change it to something meaningful and unique. This name is what will appear as a feeder's parent in the Feeders table.
4) In the wizard, use the drop-down menu to select the fiducial type (make sure it is defined on the Parts tab first).
5) Optional but highly recommended - pick some convenient point on the physical feeder group to be its origin, jog the camera over that point, align the cross-hairs, and click the Capture Camera location button to set the Feeder Groups Location and Rotation. This step is optional but useful for later checking the setup after moving a feeder group.
6) If the machine's bed is not exactly level, set the Z coordinate of the Feeder Group by manually jogging the nozzle tip down so that it just touches the physical feeder group.  Note the Z level in the DRO and type it into the Z textField.
7) Now click the "Define Fiducial Locations Using Vision" button and follow the instructions in the down camera view.
8) Click the Apply button to save the setup.
9) Now setup all the feeders attached to the feeder group as done normally. Note that this step can be done anytime after step 1 above.
10) Now change the parent of the attached feeders to be the new feeder group. To do that, just select their row(s) (multi select is ok) in the feeder table and right click for a pop-up menu and select Set Parent-><name of your feeder group from step 3>. Note that this step must only be done after step 8 above. Note that changing the parent of a feeder does not alter the feeder's location information.

The feeders can now be used as they would normally be used. Note that in order to enable a feeder, all of its ancestor feeder groups must be enabled. All descendants of a feeder group are disabled simply by disabling the feeder group. When re-enabling a feeder group, the enabled/disabled state of each of its descendants is restored to what it was prior to the feeder group being disabled.

If a feeder group is physically moved it will need to be re-aligned. To do that, select it in the Feeders tab, click the "Set Location Using Fiducials" button and follow the instructions in the down camera view. If it has moved only slightly, click the "Fine Tune Location" button to attempt an automatic alignment - it will fall back to the manual method if it can't find the fiducials near their expected locations. If the machine's bed is not level, repeat step 6 above.  Click Apply and all the locations of the descendants of the feeder group will update automatically.

It is possible for feeder groups to be children of other feeder groups (up to 32 generations deep although it's difficult to imagine anyone needing that many).

When deleting a feeder group, the parent of all its children are automatically set to the parent of the feeder group. Doing so does not alter any descendant's location information.
