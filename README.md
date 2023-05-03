Download Link: https://assignmentchef.com/product/solved-cs1027-assignment3
<br>
To gain experience with

<ul>

 <li>Solving problems with the queue data type</li>

 <li>Using inheritance to reuse &amp; modify existing code</li>

 <li>The design of algorithms in pseudocode and their implementations in Java</li>

 <li>Handling exceptions</li>

</ul>




<h1>Introduction</h1>




Halloween isn’t quite over for our intrepid adventurer from Assignment 2. After having fallen through a magical portal during his trick-or-treating, Bryan the Bold has found himself lost and without his candy! Worse yet, this strange new realm has actual monsters!

After some investigating, Bryan found a helpful Sorceress that was willing to send him back to his home, but she requires payment in candies for the spell she’s going to cast. Using your path-finding skills from last time, Bryan needs your help to figure out which parts of this strange new world are worth the risk to investigate, and which ones are not. He has some maps of locations to explore for candy, but wants to plan out whether they are safe to explore or not.

Stranger yet, when Bryan gets to the candy piles, he briefly unlocks some superpowers in this strange new realm! When he picks them up, he’s able to throw lightning bolts at the approaching monsters! Between this and some smart planning, he’s hoping to collect enough candy to pay the Sorceress for her services.

Can you help Bryan collect enough candies to return home?




<h1>Reminder: Valid Paths</h1>

When looking for a path the program must satisfy the following conditions:

<ul>

 <li>The path can go from Bryan, a cross path cell, or a candy cell to the following neighbouring cells: o A candy cell, o A cross path cell,

  <ul>

   <li>The north cell or the south cell, if such a cell is a vertical path, or</li>

   <li>The east cell or the west cell, if such a cell is a horizontal path.</li>

  </ul></li>

</ul>




<ul>

 <li>The path can go from a vertical path cell to the following neighbouring cells:

  <ul>

   <li>The north cell or the south cell, if such a cell is either Bryan, a cross path cell, a candy cell, or a vertical path cell.</li>

  </ul></li>

 <li>The path can go from a horizontal path cell to the following neighbouring cells:

  <ul>

   <li>The east cell or the west cell, if such a cell is either Bryan, a cross path cell, a</li>

  </ul></li>

</ul>

candy cell, or a horizontal path cell.







<strong>Figure 1</strong>. A sample of one of Bryan’s neighbourhood maps represented as a grid of cells

<strong> </strong>







<strong>PC vs NPC: </strong>‘PC’ means ‘Player Character’, and refers to the character usually controlled in a video game or board game. ‘NPC’ refers to Non-Player character and is controlled by the game. Here, Bryan’s token is the ‘PC’ and the Zombies are the NPCs.

<strong> </strong>

<strong>NEW NPC Pathing:</strong>




If while looking for a path the program finds that from the current cell there are several choices as to which adjacent cell to use to continue the path, your program must select the next cell for the path in the following manner:




<ul>

 <li>The NPC prefers a PC cell over all other cells.</li>

 <li>The NPC then prefers a candy cell over the other cells.</li>

 <li>If there is no candy cell adjacent to the current cell, then the NPC must prefer the cross path cell over the other cells; and</li>

 <li>If there is no cross-path cell, then the NPC chooses the smallest indexed cell that satisfies the conditions described above.</li>

 <li>NPCs do not mark their path and may end up in a loop – this is okay.</li>

</ul>

<h1>Provided files</h1>




The following is a list of files provided to you for this assignment. You do not need alter these files in any way and should assume we will mark them with unmodified ones. Studying these will help improve your understanding of Java. Some of these will be familiar from Assignment 2, and we will only go over the new methods you will need to implement your classes:

<ul>

 <li>java – This class represents the map of the neighbourhood, including Bryan’s starting location and the candy houses. New methods you may see include but are not limited to:</li>

</ul>




<ul>

 <li><em>public MapCell[] getZombieCells(int numZombies)</em></li>

 <li>This method returns the cells that Zombies will spawn in and is used in StartSearch.java to put the zombies in their starting position at the bottom of the map.</li>

</ul>




<ul>

 <li>java – This class represents the cells of the map. Objects of this class are created inside the class <em>Map</em> when its constructor reads the map file. The new methods that you might use from this class are:</li>

</ul>




<ul>

 <li>CellType getType() returns the type of the current cell, which is useful for figuring out if a PC or NPC token has collided with each other, or for getting the cell that a PC or NPC token is obscuring.</li>

 <li>void setType(MapCell.CellType) takes in one of the pre-set types (HERO,</li>

</ul>

SUPERHERO, ZOMBIE, GHOST) and sets the MapCell to be of that type. Used

when a PC or NPC token moves onto a new cell and the display needs to be updated, and the one left behind needs to be returned to its original cell type. o You may also wish to check out CellType in this class. o <strong>Forgetting to set types before and after a token moves is one of the most common causes of bugs!</strong>

<em> </em>

<ul>

 <li>java o This file has been modified from the A2 solution to handle multiple object types.

  <ul>

   <li>You should not modify this file. Code your required .java files to match and allow this class to compile.</li>

  </ul></li>

</ul>

<em> </em>

<ul>

 <li>java o This class moves the solution from A2 for finding the best cell and uses it to move the Player object around the map like before. o Studying this class and modifying it to suit NPCObject.java is strongly recommended. o You are asked to implement specific parts of this class – see below.</li>

</ul>

<em> </em>

<ul>

 <li>Other classes provided:

  <ul>

   <li><em>java, ArrayStackADT.java, QueueADT.java, CellColors.java, </em></li>

  </ul></li>

</ul>

<em>CellComponent.java, InvalidNeighbourIndexException.java, CellLayout.java, </em>

<em>InvalidMapException.java, IllegalArgumentException.java, </em>

<em>EmptyCollectionException.java, EmptyStackException.java, TestQueue.java, TestSearch.java (Updated) </em>

<em> </em>

<h1>Classes to implement</h1>




A description of the classes that you are required to implement for full marks in this assignment are given below. You may implement more classes if you want; you must submit the code for these with your assignment.

In all these classes, you may implement more private (helper) methods as desired, but you may<strong> not</strong> implement more public methods. You may<strong> not</strong> add static methods or instance variables. Penalties will be applied if you implement these.

For this assignment, you may not use Java’s <em>Queue</em> class, although reading and understanding the code there may help you better understand queues. You also may not use any other premade Java collections libraries. The data structure required for this assignment is a circular queue, described below:




<h2>CircularArrayQueue.java</h2>

<strong> </strong>

This class represents a Queue implementation using a circular array as the underlying data structure. This class must implement the QueueADT and work with the generic type (T). Note: the front index must start at DEFAULT_CAPACITY-1 and rear must start at DEFAULT_CAPACITY-2

This class must have the following <em>private</em> variables:

<ul>

 <li>front (int)</li>

 <li>rear (int)</li>

 <li>count (int)</li>

 <li>queue (T array)</li>

 <li>DEFAULT_CAPACITY (final int) with a value of 20 The class must have the following <em>public</em> methods:</li>

 <li>CircularArrayQueue (constructor) – no parameters required in this first constructor. Initialize the front to DEFAULT_CAPACITY-1, rear to DEFAULT_CAPACITY-2, count to 0, and the queue array using the final int variable as the array’s capacity.</li>

 <li>CircularArrayQueue (second constructor) – same as the first constructor described above, except that this one takes in an int parameter for the initial capacity rather than using the default capacity. Front and rear are set to initialCapacity-1 and initialCapacity-2 respectively.</li>

 <li>enqueue – takes in an element of the generic type and adds that element to the rear of the queue. If the queue is full before adding this item, then call expandCapacity.</li>

 <li>dequeue – throws an EmptyCollectionException if the queue is empty; otherwise remove and return the item at the front of the stack.</li>

 <li>first – throws an EmptyCollectionException if the queue is empty; otherwise return the item at the front of the queue without removing it.</li>

 <li>isEmpty – returns true if the queue is empty, and false otherwise.</li>

 <li>size – returns the number of items on the queue.</li>

 <li>getFront – returns the front index value (NOTE: this is not part of the QueueADT but is still required for this assignment).</li>

 <li>getRear – returns the rear index value (NOTE: this is not part of the QueueADT but is still required for this assignment).</li>

 <li>getLength – returns the current length (capacity) of the array (NOTE: this is not part of the QueueADT but is still required for this assignment).</li>

 <li>toString – returns the string containing “QUEUE: ” followed by each of the queue’s items in order from front to rear with “, ” between each of the items and a period at the end of the last item. If the queue is empty then print “The queue is empty” instead.</li>

 <li>expandCapacity (private) – create a new array that has 20 more slots than the current array has, and transfer the contents into this new array and then point the queue instance variable to this new array by resetting the front and rear appropriately. You may</li>

</ul>

set the front to 1 and the rear to count when expanding the array instead of the DEFAULT_CAPACITY based front and rear.

<h2>NPCObject.java</h2>




This class will be used to represent one or more enemy tokens on the map. It is similar to PlayerObject.java, but used to allow the enemy tokens to have unique behaviours from it.




This class must have the following <em>private</em> variables:

<ul>

 <li>private CircularArrayQueue&lt;MapCell&gt; npcMoveQueue;</li>

 <li>private MapCell cell;</li>

 <li>private MapCell.CellType onTopOfCellType</li>

 <li>private boolean heroCollision;</li>

</ul>




This class must have the following methods (some private, some public):

<ul>

 <li>public NPCObject (MapCell startCell) o Creates a new NPC object, sets cell to startCell, sets the cellType to ‘ZOMBIE’, preserves the original cell type in onTopOfCellType, and initializes the CircularArrayQueue.</li>

 <li>Private MapCell singleMove(MapCell cell) o This is a helper method used by the following method. Given a single cell, it finds the next cell that is the best path for the NPC to take. Please see the section on ‘NPC Pathing’ for specifics on what must be changed for the NPC class pathing.

  <ul>

   <li>If the NPC queues up a cell of type HERO, set heroCollision to true.</li>

  </ul></li>

 <li>Public void queueMovePlan() o Zombies are slow to react, and this method enforces that by forcing them to plan their moves 3 steps in advance.

  <ul>

   <li>When the npcMoveQueue is empty, this method should queue up the 3 next best moves given the NPC’s current spot on the map using singleMove(MapCell cell) above.</li>

   <li>When the npcMoveQueue is not empty, this method should not adjust or interact with the queue in any way.</li>

  </ul></li>

 <li>Public void move() o This represents the zombie moving. You’ll find that the zombie can find a pair of cells that it moves back and forth between – this is okay, they are zombies and can often get stuck in patrols.

  <ul>

   <li>This method dequeues the moves from queueMovePlan (one at a time per iteration of the loop in StartSearch.java)</li>

   <li>Make sure to update the cell types once the NPC has moved from a square (back to its original type) to the new one (temporarily updated to ZOMBIE)</li>

  </ul></li>

 <li>Public Boolean checkHeroCollision(), publicMapCell getCell() &amp; public MapCell.CellType getCellType() — These are all getters for the variables in the class.</li>

</ul>




<h2>AdvancedPlayerObject.java</h2>




This class must inherit from Player object.

This class must have the following <em>private</em> variables:

<ul>

 <li>Private Boolean collision</li>

 <li><em>Remember that as an inherited class it can use all of the parent class variables that are available to it!</em></li>

</ul>

This class must have the following methods:

<ul>

 <li>Public AdvancedPlayerObject(MapCell startCell) o Follows the usual rules for inherited constructors

  <ul>

   <li>Suggested (not required, there are other ways to solve) to set onTopOfCellType</li>

  </ul></li>

</ul>

= MapCell.CellType.SUPERHERO

<ul>

 <li>If you don’t have an issue getting the ‘Superhero’ icon to display this may not be required for your solution.</li>

</ul>

<ul>

 <li>Public MapCell getMove(MapCell newCell) o The advanced player object functions a bit differently than the normal one.

  <ul>

   <li>Firstly, it doesn’t move, it only attacks.</li>

   <li>This method will check all neighbours to see if they are NPC objects and smite the nearest one, using the index order when there are multiple options</li>

   <li>If there are none in the neighbours, all of the neighbours <strong>of </strong>the neighbours are also checked.</li>

  </ul></li>

 <li>Public void smiteZombie(MapCell zombieCell, NPCObject[] zombieArray) o This method is used to imitate ‘attacking’ one of the NPCs once the Hero token has moved onto a candy tile.

  <ul>

   <li>Given a tile that has a zombie, find which entry in zombieArray corresponds to it, and then delete that zombie from the array. The model solution turns the entry to null, but there may be other ways to do this if you wish to investigate.</li>

   <li>Print out an indication that an NPC was smote, and the identifier of the cell where it happened.</li>

  </ul></li>

</ul>




<h1>Command Line Arguments</h1>

Your program must read the name of the input map file from the command line.

You can run the program with the following command:

<strong><em>java StartSearch nameOfMapFile maxPathLength numberOfZombies </em></strong>Where nameOfMapFile is the name of the file containing the desert map, and maxPathLength is the longest path that Bryan can take to find candies, and numberOfZombies is how many Zombies to spawn.







You can access run configurations as follows:




In the text box for ‘Program arguments’, you can type your arguments in. Ex: a3map1.txt 20 2, for running a3map.txt with a maximum path length of 20 and spawning 2 zombies. Note that the program sets a maximum amount of zombies based on the map size.

<h1>Image Files and Sample Input Files Provided</h1>

<ul>

 <li>You are given several image files that are used by the provided Java code to display the different kinds of map cells on the screen.</li>

 <li>You are also given several input map files that you can use to test your program.</li>

 <li>In Eclipse put all these files inside your project file in the same folder where the src folder is.</li>

 <li>Do not put them <strong>inside</strong> the src folder as Eclipse will not find them there.</li>

 <li>If your program does not display the map correctly on your monitor, you might need to move these files to another folder, depending on how your installation of Eclipse has been configured.</li>

</ul>

<h1>Marking notes</h1>




Marking categories

<ul>

 <li>Functional specifications o Does the program behave according to specifications? o Does it produce the correct output and pass all tests? o Are the class implemented properly?

  <ul>

   <li>Are you using appropriate data structures?</li>

  </ul></li>

 <li>Non-functional specifications o Are there Javadocs comments and other comments throughout the code? o Are the variables and methods given appropriate, meaningful names? o Is the code clean and readable with proper indenting and white-space?

  <ul>

   <li>Is the code consistent regarding formatting and naming conventions?</li>

  </ul></li>

 <li>Penalties o Lateness: 10% per day

  <ul>

   <li>Submission error (i.e. missing files, too many files, ZIP, etc.): 5% o “package” line at the top of a file: 5%</li>

  </ul></li>

</ul>




Remember you must do all the work on your own. Do not copy or even look at the work of another student. All submitted code will be run through cheating-detection software.


