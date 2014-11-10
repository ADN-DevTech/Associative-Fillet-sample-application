Associative-Fillet-sample-application
=====================================

A realistic Associative Fillet ObjectARX sample application

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

Building the sample application:

Please copy all source files into a new arxsdk\samples\entity\AssocFillet 
directory in order to be able to build the project. AssocFillet.vcxproj references 
files in arxsdk\inc and the source files need to be placed in a second-level 
subdirectory under arxsdk\samples directory.
