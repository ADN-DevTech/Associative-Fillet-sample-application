Copyright 2014 Autodesk, Inc.  All rights reserved.

Use of this software is subject to the terms of the Autodesk license 
agreement provided at the time of installation or download, or which 
otherwise accompanies this software in either electronic or hard copy form.   

Description: 

This sample ARX application implements a new AssocFilletActionBody action 
that maintains an associative fillet arc between two selected entities (such 
as lines or circles) or subentities of entities (such as segments of polylines). 
When the input geometries change or the fillet radius changes, the fillet arc 
automatically updates and the input geometries are re-trimmed. 
See the description in the AssocFilletActionBody.h header file for more details.

The new ASSOCFILLET command can be used to create new associative fillets, or
to edit the existing ones (when selecting an existing associative fillet arc
entity instead of a general entity). See the implementation of the 
assocFilletCommandUI() function in the AssocFilletCommandUI.cpp file.

The main files to look at:

AssocFilletActionBody.h   ... Declaration    of the AssocFilletActionBody class
AssocFilletActionBody.cpp ... Implementation of the AssocFilletActionBody class
AssocFilletCommandUI.cpp  ... Simple command-line UI

Steps to try the associative fillet functionality:

- Command: APPLOAD, load the AssocFillet.arx application
- Create two intersecting lines in AutoCAD
- Command: PARAMETERS, create new parameters Trim1 and Trim2 with value 0
- Command: ASSOCFILLET, follow the prompts, enter non-zero radius and use Trim1 
  and Trim2 as the expressions to control whether to trim/extend the input lines
- Change the color of the fillet arc to Green
- Command: PARAMETERS, change value of Trim1 to 1, and then Trim2 to 1, see what happens
- Select end grip point on one of the lines, drag the grip point. See how the dragged 
  line behavior changes due to the fillet, and the fillet keeps updating
- Command: PARAMETERS, create a new parameter named A, assign it a value, such as 3.0, 
  create a new parameter named Radius, assign it an expression, such as “A/2"
- Command: ASSOCFILLET, select the associative fillet arc, change radius to be 
  an expression, such as “FilletRadius=Radius+0.1“
- Command: COPY, select the two input lines, but not the associative fillet arc, 
  make two copies. See that the associative fillet arc has been copied and stays associative
- Command: PARAMETERS, change value of parameter A, see that all associative fillets update
- Command: ELLIPSE, create two intersecting ellipses, one horizontal, another vertical
- Command: ASSOCFILLET, create a fillet at one of the 16 possible positions
- Grip-edit one of the ellipses, see that the associative fillet stays
- Move one ellipse, see that that associative fillet stays
- Draw two polylines with several segments
- Command: ASSOCFILLET, selects two segments of the two polylines using <Ctrl> selection
- Drag one polyline, see that the associative fillet updates
- Delete and insert some polyline segments. See that the associative fillet stays 
  attached to the same segments even if the number of the segments changed – the fillet 
  stores AcDbAssocPersSubentIds of the polyline segments
- Command: EXTRUDE, select the input lines and the fillet arc, specify extrusion 
  height by expression, such as “3*A”
- Command: PARAMETERS, change value of parameter A. See that the associative fillets updates, 
  followed by the update of the extrusion surface that depends on the three entities (the 
  two lines and the fillet arc). The input lines and the fillet arc have two actions 
  attached to them: The associative fillet action as well as the extrusion action
- Drag one of the lines. See that the fillet as well as the extrusion surface update
- Command: ASSOCFILLET, select a fillet, change radius to 0.0 – becomes associative trim
- Command: ERASE, select one of the lines. See that the associative fillet arc is also erased
- Command: UNDO to bring the associative fillet back
- Command: PARAMETERCOPYMODE, enter 4 to copy all referenced parameters
- Command: WBLOCK, select one pair of input lines
- Open a new drawing
- Command: INSERT, choose the drawing created by the WBLOCK command, make several inserts
- Command: EXPLODE, select a few block references
- See that the associative fillet is there, as well as the parameters it depends on



