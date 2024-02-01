# Pack-in Records

Pack-ins are an evil system to make a simple deployable object of complex arrangement of pieces. For example in Galactic Junk Recycler I use a Vending machine and 2 chests in a pack-in and a constructable object can deploy the pack-in.

## Pack-in Flags
- Prefab will almost always be on a packing
- Unknown11 bulldozes ground so the packin can be placed.
  - This also turns everything in the packing to a single static object so it will break triggers/activators/terminal/NPCs/etc.
  - If you need activator type objects just put another packin in the main packin to serve as a foundation layer and only the foundation layer packing should have unknown11 on it. 

## Pack-in Cells

Pack-ins use a fake world space and a semi weird random coordinate system based on a placeholder dummy object. It would make sense if the coordinates always started from 0,0,0 but they don't. So the best way I have found is to properly wire up the pack-in to a constructable object with a waste bin/storage container in it and keep moving the coordinates around until you see it in the real world. Then use console modpos/modangle to move/rotate the object where you want you piece recording all the movements. Then add those coordinate changes to the waste bin in the fake world space and redeploy making sure it ended up where you wanted it. Then replace the waste bin with your real object and fix the rotations. Finally rinse and repeat for any other objects you need in the pack-in.

Another possibility I haven't fully tested yet is to use the FastTravel(FT) console command to teleport into the pack-in cell. This should make coordinates of object match in the cell and xEdit speeding content creation.  The fact that a lot of pack-in cells have unneeded XMarkers means the BGS team probably used this method too. You need add a persistent object with form ID 34, make sure its position land on a fixed object or you will go into endless falling. The pass the REFR FormID to FT. 
