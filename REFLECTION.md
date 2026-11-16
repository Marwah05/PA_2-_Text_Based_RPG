1.
TODO 1: Scene constructor. It allocates dynamic array pointers to numChoices_. It also initializes each slot to nullptr.
If the choices are 0 or under, then it treats it as an ending scene and sets the choices to nullptr. The complexity is 
O(1) because at most a scene has 3 slots only.

TODO 2: Scene destructor. It uses recursive methods to free heap memory by deleting every child scene pointer in 
choices_. It also deletes the array itself and its stored data_ objects. The time complexity is O(n) when called on 
root because every scene is deleted once.

TODO 3: isEnding. It returns true if the number of choices is 0, meaning it reached an ending scene. The complexity 
is O(1).

TODO 4: getChoice. It bound checks the given index and returns its child scene pointer at that index or the nullptr.
The time complexity is O(1).

TODO 5: setChoice. Also bound checks the index and assigns a child scene to its pointer slot. The time complexity is  
O(1).

TODO 6: countScenes. It recursively counts all scenes in the subtree starting from the node its at by adding 1 to the
child count. The time complexity is O(n) because it's the number of the scenes in the story.

TODO 7: countEndings. It recursively traverses through the tree to count how many nodes meet the "isEnding()" function.
Its time complexity is O(n) because of that.

TODO 8: height. Recursively calculates the maximum depth of the tree from the current scene its at till the ending. Its
time complexity is O(n).

TODO 9: StoryTree::clear. Deletes the root scene and sets root_ to nullptr. Its complexity is O(n).

TODO 10: Adventure::load. This opens the story file to read its starting HP, then readScene to parse through the tree.
It also attaches the root, making it a complexity of O(n) because it's proportional to the scene size.

TODO 11: Adventure::readScene. It reads every scene field such as scene, hp, loot, item, and choices, alongside its
child label scenes and checking their limits. Its complexity is O(n).

TODO 12: Adventure::askChoice. Asks the user for a valid input in a loop. Its complexity differs based on the amount of 
user inputs, it could be 1 to however many needed. It's O(1) per attempt though.

TODO 13: Adventure::play. It executes the gameplay loop and manages all sorts of changes from hp to scene transitions.
Its complexity is O(x) where x is the length of actual playthrough path.

TODO 14: printStats. It calls the tree methods to print the total scenes, endings, and maximum playthrough height. Its 
complexity is O(n).

TODO 15: printSpoilers. It just initiates a recursive call to print all the endings from the root. The complexity is 
O(n).

TODO 16: printEndings. Also a recursive call to print all the endings and the choice paths. O(n) complexity.

TODO 17: greedyRun. It simulates a playthrough by picking the child branch with the highest loot immediately. Its big O 
would be O(x) where x is the depth of that path.

TODO 18: bestLoot. Also recursively explores every valid path using DFS in order to get the maximum possible loot 
amount without going below 0 HP. Its big O is O(n).

TODO 19: optimalRun. It executes bestLoot from the root and prints the optimal path, maximum loot, or failure status. 
Its complexity is O(n).

2. The reason for using a dynamic array instead of declaring Scene<T>* choices[3] is because it would make every scene 
have 3 choices no matter what. Some endings require 0 choices to be an ending, and some have only 1 or 2, this method 
would waste memory (Scene<T>* choices[3]). The ending holds in choices_ because it holds nullptr in choices_. This 
properly signifies that there are no more choices to branch out to for the program.

3. Children are deleted first, using numChoices_ - 1 so that it starts form i = 0 and deletes on each one. So it deletes
 the immediate children first, then goes recursively to the ones below. Afterward the array is deleted, so the pointer
 itself gets deleted. Lastly, it's the data that's deleted. If choices_ was deleted first then that would cause then the
 pointer array holding the address of each child scene would be deleted first. This would cause for a loss of reference
 for those child nodes, causing a memory leak.

4. In my story, the greedy fails because it chooses to go for the highest loot amount, therefore going to the Ruby Hall
 and immediately hitting the lethal traps of poking the dragon or picking the wrong altar item. This causes greedy to
 just die mid-way. As for the optimal path, it uses bestLoot to look ahead across all the paths, skipping the ones
 leading to death and successfully getting to a good ending with the highest amount of loot.

5. bestLoot basically explores multiple branches recursively, but since this is a tree, each path it tries has only one 
parent, which makes for one path for each scene. Unlike actual recursive problems that have problems within subproblems,
 every node in our story is visited a constant number of times during our traversal. Since each one of those is O(n),
 scenes and evaluated once per traversal, it ends up with the complexity O(n).

6. The game uses bag.search(*newItem) and bag.addFront(newItem). The first one checks whether the item is already in 
the inventory, while the second adds the new item to the front of the list. These are used to make sure that the items 
within the bag are not duplicates and so that they could be dynamic. The picking up an item is just O(1) since it adds 
it to the front, while the search one would increase over time, making O(x), x being the items in the bag. 
