

                   The Walrus Graph Visualization Tool

                              version 0.6.3

                               Mar 30, 2005

                      (c) 2000,2001,2002 CAIDA/UCSD

            (http://www.caida.org/tools/visualization/walrus/)
                      Young Hyun <youngh@caida.org>


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
DESCRIPTION

Walrus is a tool for interactively visualizing large directed graphs in
three-dimensional space.  It is technically possible to display graphs
containing a million nodes or more, but visual clutter, occlusion, and
other factors can diminish the effectiveness of Walrus as the number of
nodes, or the degree of their connectivity, increases.  Thus, in practice,
Walrus is best suited to visualizing moderately sized graphs that are
nearly trees.  A graph with a few hundred thousand nodes and only a
slightly greater number of links is likely to be comfortable to work with.

Walrus computes its layout based on a user-supplied spanning tree.  Because
the specifics of the supplied spanning tree greatly affect the resulting
display, it is crucial that the user supply a spanning tree that is both
meaningful for the underlying data and appropriate for the desired insight.
The prominence and orderliness that Walrus gives to the links in the
spanning tree, in contrast to all other links, means that an arbitrarily
chosen spanning tree may create a misleading or ineffective visualization.
Ideally, the input graphs should be inherently hierarchical.

Walrus uses 3D hyperbolic geometry to display graphs under a fisheye-like
distortion.  At any moment, the amount of magnification, and thus the level
of visible detail, varies across the display.  This allows the user to
examine the fine details of a small area while always having a view of the
whole graph available as a frame of reference.  Graphs are rendered inside
a sphere that contains the Euclidean projection of 3D hyperbolic space.
Points within the sphere are magnified according to their radial distance
from the center.  Objects near the center are magnified, while those near
the boundary are shrunk.  The amount of magnification decreases
continuously and at an accelerated rate from the center to the boundary,
until objects are reduced to zero size at the latter, which represents
infinity.  By bringing different parts of a graph to the magnified central
region, the user can examine every part of the graph in detail.


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
CHANGES

Since 1.0.1, released Jun 10, 2019:

  * Switched deprecated Oracle Java3d 1.5 package to Java3d 1.6 package from Jogamp
  * Modified Java3d package into custom version to fix the rendering bug
  * Ported walrus from java 1.6 to java 1.8

Since 0.6.2, released Feb 20, 2003:

  * No changes to any functionality; just a licensing change to the GPL.
  * Added 'palmtree.graph' to set of sample graphs.

Since 0.6.1, released Nov 4, 2002:

  * Corrected equation for computing colors in guide.txt.
    No new features.

Since 0.6, released Apr 29, 2002:

  * Re-implemented routines for hyperbolic transformations.
    No new features.  Everything should work exactly as for v0.6.

Since 0.5, released Apr 19, 2002:

  * Added support for zooming the display.
       The user can zoom in toward the central node or zoom out from it
       to an arbitrary degree.
  * Added support for turning depth cueing off.
  * Fixed bug in which picking would sometimes become temporarily
    inaccurate after the window is resized.
  * Fixed bug in which the display would lock up if the user executed
    a command through the keyboard while concurrently interacting with
    the mouse.

Since 0.4, released Apr 12, 2002:

  * Added support for temporarily hiding parts of the graph.
       For example, the user can display only the subtree rooted at the
       current central node.  It should now be much easier to navigate
       and examine large complicated graphs, since occlusion can be
       eliminated by selective pruning.
  * Added code to detect and warn about malformed spanning trees.
  * Added support for quickly navigating to the parent of the current
    central node.
  * Added support for resetting the rendering state.
       Loss of floating-point precision can cause the display to become
       wholly useless.  This sometimes happens while navigating very large
       graphs.

Since 0.3, released Apr 1, 2002:

  * Added support for computing the layout using extended precision
    arithmetic (about 30 decimal digits of precision).
      Previously, the layout calculations would sometimes yield invalid
      coordinates (NaNs) for some tall and bushy graphs.  This problem
      went unnoticed because Java does not throw floating-point exceptions.

Since 0.2, released Jan 25, 2002:

  * Added some more introductory documentation on the LibSea file format.
      This should help people to get up to speed quickly. See docs/guide.txt.
  * Added support for overlaid node labels.
      Attribute values can now be shown in the display area next to the
      relavant nodes.  These labels, however, are only temporary and
      disappear once the user moves or refreshes the window.
  * Added support for selection attributes.
      A boolean attribute in the graph file can be used to specify which
      nodes or links are to be displayed.
  * Added support for displaying attributes of list type.
      Previously, only scalar attributes could be displayed.
  * Improved the layout of binary trees.
      Walrus now makes better use of available space when laying out
      binary trees.
  * Fixed bug in which links would sometimes be drawn as black lines.
      If you had transparency enabled and then switched the coloring of
      links to RGB (that is, to colors stored in an attribute), then
      links would sometimes be drawn incorrectly as black lines.
  * Fixed bug in which rotations would stop working when axes were
    disabled while running the nonadaptive render loop.

Since 0.1, released Dec 5, 2001:

  * Re-implemented the picking algorithm.
      Picking is now more accurate and intuitive in behavior.
  * Added full support for color to the nonadaptive render loop.
      The nonadaptive render loop is active when Rendering->Adaptive
      Rendering is unchecked.
  * Fixed a refresh bug.
      The display would sometimes fail to refresh when the user clicked
      within the Walrus window to bring it to the front.


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
REQUIREMENTS

Walrus requires JDK 1.8.0 (or later).

JDK:     <http://java.sun.com/j2se/>

A hardware-accelerated graphics card is necessary for adequate performance.
It is also useful to have a speedy machine with lots of memory (128MB is
probably a minimum; 256MB or more is better; 512MB is probably required
for a few hundred thousand nodes).

Windows 2000 users: Be sure to use the OpenGL version of Java3D and not the
DirectX version, which has problems on this platform.

Linux users: We, as well as others, have had problems running Java3D on
an NVIDIA card.  Using JDK 1.4 and Java3D 1.3.1beta seems to help, but
you may still experience instability.

Walrus was developed and tested on a Sun Ultra 60 with an Elite 3D card
and 512MB of RAM, running Solaris 7, a box graciously donated by Sun.


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
DOCUMENTATION

See the 'docs' subdirectory for documentation.  In particular, the file
'guide.txt' contains a brief guide to using Walrus (see also QUICK START
below) and provides details on the input file format.


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
CONTACT INFORMATION

To report bugs, email walrus-bugs@caida.org.  For general inquiry, email
walrus-info@caida.org.

A mailing list is available to discuss Walrus use and development.
To subscribe, email walrus-dev-request@caida.org with

   subscribe your-email-address

in the body (for example, 'subscribe foo@bar.com').  To unsubscribe,
email walrus-dev-request@caida.org with

   unsubscribe your-email-address

in the body.  All messages to the list itself should be sent to
walrus-dev@caida.org.

Alternatively, you may use the following web page to subscribe, unsubscribe,
view the archives, and so on:

   <http://login.caida.org/mailman/listinfo/walrus-dev>


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
QUICK START

You can give Walrus a quick try by doing the following:

1. Extract 'walrus-1.0.1.tar.gz' or 'walrus-1.0.1.zip' anywhere you wish.
   This will create a subdirectory named 'walrus-1.0.1' containing several
   JAR files, among other things.

    For UNIX users...

      The file walrus-1.0.1.tar.gz was packaged with the standard TAR utility
      and compressed with GNU GZIP (http://www.gzip.org).  You can unpack
      it with the following command:

          gzip -cd walrus-1.0.1.tar.gz | tar xvf -

    For Windows users...

      The file walrus-1.0.1.zip was packaged in the common ZIP format.  You
      can unpack it using a program like WinZip (http://www.winzip.com/).
   1.1 Download lib.zip for all jar dependencies from here 
   (https://github.com/WenlinMao/walrus/releases/tag/walrus-1.0.1)
   and place it under the 'walrus-1.0.1' subdirectory.

2. From the 'walrus-1.0.1' subdirectory, enter the following at a shell
   or command prompt:

     * on UNIX systems with Sun's JDK:

         java -cp lib/*:. H3Main

         (Or execute the supplied script: ./walrus)

     * on Windows with Sun's JDK:

         java -cp lib/*:. H3Main

3. Select the menu item File->Open (that is, 'Open' under the 'File' menu),
   and load the file 'champagne.graph' in the 'samples' subdirectory.
   The window will be blank while the file loads.  This graph has
   9175 nodes, 9174 tree links, and 6345 nontree links.  This should
   load in a few seconds, but it can take up to several minutes to load
   larger graphs.

4. Select Rendering->Start, once the Walrus logo reappears.

5. Click and drag with the left mouse button to rotate the display.
   It is normal for parts of the graph to disappear during rotations.
   Walrus uses an adaptive rendering algorithm that tries to maintain
   a given framerate (currently hardcoded) by rendering only as much as
   it can within each time slot.

6. Click on a node (yellow square) with the right mouse button to bring
   the node to the center.  Parts of the graph may disappear during
   these translations because of adaptive rendering.

7. Select Color Scheme->Predefined->Green-Olive-[Summer Sky].

8. Select Rendering->Update.

At this point, you should have a display with nodes in green, tree links
in olive green, and nontree links in a cobweb-like transparent blue.  Using
transparency like this is often a good way of exploring graphs with nontree
links.

Another feature you may wish to try is continuous rotation.  To activate
continuous rotation, hold down the control key and click the left mouse
button anywhere in the window.  Now simply move the mouse (without pressing
or holding down any buttons or any keys) to change the direction and speed
of the rotation.  The rotation vector is determined by the position of the
mouse pointer relative to the center of the window.  To stop the rotation,
click anywhere in the window with the left mouse button.

There are a number of ways of hiding parts of the graph temporarily.
Selective hiding is indispensable for navigating and examining complicated
graphs.  The Display menu contains the full list of operations for hiding
and revealing parts of the graph.  There are also convenient key bindings
for some of these.  Suppose, for example, that you wanted to focus your
attention on a single subtree.  You could hide all of the graph except that
subtree by first right clicking on the root node of the subtree (to bring
it to the center of the display) and then choosing Display->Narrow To
Subtree.  If the subtree was large and tall, you could hide all but the
descendants that lie within a certain distance from the root node of the
subtree to reduce the clutter and occlusion.  You could do this by either
choosing an item from the menu Display->Prune To Neighborhood or by
pressing one of the keys '0' to '9'.  Pressing '2', for example, would hide
all but the descendants that lie within two hops of the root node.

For examining a graph in greater detail, zooming is helpful.  Choosing
Display->Zoom In (or pressing the key '.' [the same key as for '>']) will
cause the display to zoom in toward the node at the center of the display.
You can do this as many times as you want; each time increases the
magnification of the display by 25%.  Conversely, you can zoom out one step
with Display->Zoom Out (or by pressing the key ',' [the same key as for
'<']), and reset the display to normal magnification with Display->Zoom 1:1
(or by pressing the key '/').

As mentioned earlier, Walrus uses an adaptive rendering algorithm that
tries to maintain a given framerate.  You may try out the nonadaptive
rendering algorithm for comparison by de-selecting Rendering->Adaptive
Rendering and then selecting Rendering->Update.  The nonadaptive
algorithm can be more responsive and produce a smoother display for
smaller graphs.

See 'guide.txt' in the 'docs' subdirectory for information on additional
commands and menus not covered here.


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
BUILDING AND RUNNING

The following process is for Mac OS X 10.14.5 users:

1. Download the source code from the following link:

     <https://github.com/WenlinMao/walrus/releases/tag/walrus-1.0.1>

   It is available as walrus-1.0.1-src.tar.gz or walrus-1.0.1-src.zip. You
   may unpack walrus-1.0.1-src.tar.gz by using the following command:

         gzip -cd walrus-1.0.1-src.tar.gz | tar xvf -

   The walrus-1.0.1-src.zip can be unzipped using a program of your choice.

   By unpacking either walrus-1.0.1-src.tar.gz or walrus-1.0.1-src.zip, a
   subdirectory called 'walrus-1.0.1-src' will be created. This directory,
   walrus-1.0.1-src, will have three JAR files (antlrall-mod.jar,
   libsea.jar, mp.jar) that will be mentioned later. The subdirectory of
   walrus-1.0.1-src named 'Walrus' contains the source code.

   Alternatively, you may download the source code from this link:

     <https://github.com/CAIDA/walrus>

   However, you must install three JAR files (antlrall-mod.jar, libsea.jar,
   mp.jar) from the Walrus release package.

   In this section, the directory containing the source code will be further
   referred to as the Walrus directory.

   1.1 Check within folder "/Library/Java/Extensions" to make sure all old java3d package has been removed to avoid package conflict. 
   1.2 Download lib.zip for all jar dependencies from here 
   (https://github.com/WenlinMao/walrus/releases/tag/walrus-1.0.1)
   and place it under the 'walrus-1.0.1' subdirectory.

2. Ensure that your machine is using Apple's JDK 1.8 which can be
   downloaded from <https://support.apple.com/kb/dl1572>. If your default JDK
   is not Apple's JDK 1.8 and that is the only JDK of version 1.8 that you
   have, define the Java home environment variable to Apple's JDK 1.8.

         export JAVA_HOME=$(/usr/libexec/java_home -v 1.8)

   If your default JDK is not Oracle's JDK 1.8 and you have multiple JDKs of
   version 1.8, examine all JDKs you have installed.

         /usr/libexec/java_home -V

   The above command will output a list of your JDKs with the version of
   each JDK listed as the first part on each line. Determine the version for Oracle's JDK 1.8 and define the Java home environment variable to that specific JDK. For example, if the version for Apple's JDK was 1.8.0_111, the command would look like this:

        export JAVA_HOME=$(/usr/libexec/java_home -v 1.8.0_111)

3. In your Bash shell from the Walrus directory, include the current
   directory and the path to each of the three JAR files in the classpath
   environment variable. If each jar file was one directory above the
   Walrus directory, the command would be:

         export CLASSPATH="lib/*:."

4. From the Walrus directory, run this command to build Walrus:

         make

5. From the Walrus directory, run Walrus with the -cp option to specify the
   path to all three JAR files and the current directory to search for
   classes. If all three JAR files were in the Walrus directory, the
   command would be:

         java -cp lib/*:. H3Main
    
    5.1 If terminal reports error such as no package or method found, try
    copy all Java3d releated package from lib to "/Library/Java/Extensions". 

    Java3d related packages are: j3dcore.jar, j3dutils.jar, vecmath.jar, jogamp-fat.jar

6. If you wish to build a JAR file to distribute, run the following
   command:

         make jar

   The created JAR file will be called 'walrus.jar'. To run Walrus with
   walrus.jar, follow the instructions in the Quick Start section.

   This command currrently not working as the building tool cannot
   correctly recognize libsea.jar


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
SAMPLE GRAPHS

The directory 'samples' contains the following sample graphs.

 * simple.graph
    [15 nodes, 17 links; 2 attributes]

     You may want to browse this file to see what a minimal input file
     looks like.  The '@...=' text strings are simply comments, and though
     they make debugging easier, they are not significant nor required (see
     champagne.graph for an example of an input file without these).

 * walrus-directory.graph
    [1103 nodes, 1105 links; 12 attributes]

     A graph file generated from the UNIX directory tree containing the
     Walrus source files.  This was generated using the perl scripts
     included in 'walrus/docs/dirgraph'.

     Many of the values shown in a directory listing are included in this
     graph file as attributes.  For example, the attribute 'full_name'
     contains the complete path of each file, and the attribute 'size'
     contains the file size.  To see the values of these attributes, do the
     following.  After loading the graph, select the attributes you would
     like to examine from the 'Node Label' menu.  Then choose the menu item
     Rendering->Update (and Rendering->Start, if rendering has not been
     started).  Now click on a node with the middle mouse button (or the
     right mouse button while holding down the shift key) to see the
     attributes values in the status bar at the bottom of the window.

     The graph also contains two attributes, 'mtime_color' and
     'size_class_color', which can be used to color nodes.  For example,
     to color nodes by their modification time, first select
     Color Scheme->Node Color->RGB, and then
     Color Scheme->Node Color->Color Attribute->mtime_color.  Now choose
     Rendering->Update (and Rendering->Start, if needed).

 * champagne.graph
    [9175 nodes, 15519 links; 2 attributes]

     An Internet topology graph generated from data collected by a skitter
     monitor (<http://www.caida.org/tools/measurement/skitter/>).

 * palmtree.graph
    [3652 nodes, 3651 links; 2 attributes]

     A graph contributed by Robert Hubley <rhubley@systemsbiology.org>.
     This organic looking graph, with an extremely long "trunk", nicely
     demonstrates the support in Walrus for extended-precision layout
     calculations.  It would be impossible to lay out "tall" graphs like
     this with even double precision values.


The extension '.graph' is only a convention employed in these sample graphs
and is not a requirement of Walrus.


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
ACKNOWLEDGEMENTS

Walrus was originally developed by Young Hyun at the University of California,
San Diego under the Cooperative Association for Internet Data Analysis (CAIDA)
Program.  Support for this effort was provided by NSF grant ANI-9814421,
DARPA NGI Contract N66001-98-2-8922, Sun Microsystems, and CAIDA members.

CAIDA's LibSea graph library distributed with Walrus uses the excellent and
free ANTLR parser generator (see <http://www.antlr.org>).  The file
'antlrall-mod.jar' is ANTLR 2.7.1, slightly modified to improve parsing
time (specifically, the use of Class.newInstance() to allocate token
objects was replaced with a compile-time object-allocation expression).
The modifications reduced parsing time by 1-3 minutes (corresponding to a
30-50% reduction) on 50-80MB files.

Walrus uses the MPJAVA arbitrary-precision arithmetic package, which is
a Java implementation of the arbitrary-precision package written by
David H. Bailey, et al; see <http://www.nersc.gov/~dhb/mpdist/mpdist.html>.
MPJAVA was written by Siddhartha Chatterjee and Herman Harjon; see
<http://www.cs.unc.edu/Research/HARPOON>.
