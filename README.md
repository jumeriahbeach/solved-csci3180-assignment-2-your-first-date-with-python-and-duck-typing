Download Link: https://assignmentchef.com/product/solved-csci3180-assignment-2-your-first-date-with-python-and-duck-typing
<br>
The purpose of this assignment is to offer you the first experience with Python, which supports the Object-Oriented programming paradigm. Our main focuses are Dynamic Typing and Duck Typing. Please use Python <strong>3.6 </strong>to finish this assignment.

The assignment consists of 4 tasks.

<ul>

 <li>You need to implement a famous board game called Six Men’s Morris in Python.</li>

 <li>You are asked to demonstrate the advantages/disadvantages of dynamic typing through some example code, which could be taken from any code you write for this assignment.</li>

 <li>We give you the Java source code of a game called “Save The Tribe”. You need to reimplement the game in Python to make the code cleaner with the help of Duck Typing.</li>

 <li>Additional features and mechanisms are introduced to the “Save The Tribe” game. You need to implement the enhanced game in both Java and Python.</li>

</ul>

After completing the 4 tasks, you need to write a report elaborating on Dynamic Typing and Duck Typing.

<strong>NOTES: </strong>all your codes will be graded on the Linux machines in the Department. You are welcome to develop your codes on any platform, but please remember to test them on Department machines.

<h1>2         Task 1: Six Men’s Morris</h1>

This is a programming exercise for you to get familiar with Python, which is a dynamically typed language. In this task, you have to strictly follow our proposed OO design and the game rules for the 2-player “Six Men’s Morris” game stated in this section.

Six Men’s Morris is a popular game in Italy, France and England during the Middle Ages but was obsolete by 1600. You can have a try to play this game in <a href="https://www.novelgames.com/en/sixmensmorris">https://www.novelgames.com/ </a><a href="https://www.novelgames.com/en/sixmensmorris">en/sixmensmorris</a><a href="https://www.novelgames.com/en/sixmensmorris">.</a>

For simplicity, we want you to implement a watered-down version of Six Men’s Morris. The detailed specification or game rules are described as follows.

<h2>2.1     Description</h2>

The game board consists of a grid with 16 intersections or <strong>points </strong>as shown in Figure 1. Each player has <strong>six pieces</strong>, or “men”, coloured <strong>black </strong>or <strong>white</strong>. Players try to form “<strong>mills</strong>”— <strong>three of their men lined up horizontally or vertically</strong>—allowing a player to remove the opponent’s man from the game board. For simplicity, Player 1 always uses the <strong>white </strong>pieces and Player 2 uses the <strong>black </strong>ones.

The game proceeds in the following two phases.

<ol>

 <li><strong>Placing the pieces. </strong>The game begins with an empty board. Player 1 first starts to play and the two players take turns placing their men, one per turn on empty points. This phase will last for 6 rounds since each player has only 6 men. Note that a player forming a mill can remove one of the opponent’s pieces from the board. However, <strong>no one can win during Phase 1</strong>. After all men are placed, Phase 2 begins.</li>

</ol>

Figure 1: Game board for Six Men’s Morris.

<ol start="2">

 <li><strong>Moving the pieces. </strong>Players again alternate moves, this time moving a man to an <strong>adjacent and unoccupied point</strong>. A piece may not “jump over” another piece. Players continue to try to form mills and remove their opponent’s pieces as in Phase 1. Note that a player can “break” a mill by moving one of his pieces out of an existing mill, then moving it back to form the same mill a second time (or any number of times), each time removing one of his opponent’s men.</li>

</ol>

<strong>Game goal or winning conditions. </strong>A player wins by reducing the opponent to <strong>two men </strong>(where the opponent could no longer form mills and thus be unable to win), or by <strong>leaving the opponent with no legal moves</strong>. Note that <strong>this game will never end in a tie</strong>.

As shown in Figure 2, on the left-hand side, Player 1 loses the game because (s)he has only two pieces left. On the right-hand side, Player 1 also loses the game because (s)he cannot move any one of the white pieces.

Figure 2: Winning conditions of Six Men’s Morris. A player wins by reducing the opponent to <strong>two pieces </strong>or by <strong>leaving them without a legal move</strong>.

<strong>Mill examples. </strong>As shown in Figure 3, the left board forms a mill since three black pieces are <strong>lined up horizontally</strong>. The right board forms no mill because there are no lines between the lower two pieces.

Figure 3: Visualization of a mill. Mill is formed when three men of the same color are lined up horizontally or vertically.

<h2>2.2      Problem Specification</h2>

This section describes the requirements, program design, function decomposition, game flow, etc.

<strong>2.2.1         Game Board Representation</strong>

There are 16 possible points on a board. Therefore, we use letters <em>a,b,c,…,p </em>to denote these board positions, as illustrated in Figure 4.

Figure 4: Board positions specification.

To encode the whole game board, we use an array of 16 characters. Each character in the array is either “.” (Empty point), “#” (Player 1), or “@” (Player 2). Using this representation, the initial board is encoded as an array of 16 “.” characters.

<strong>2.2.2         Input/Output Specification</strong>

<strong>Types of Player. </strong>Users can choose Player 1 and Player 2 to be either human- or computercontrolled. You have to use the command line to request the types of the two players before starting the game (as shown in Figure 5).

Figure 5: Setting for the type of players.

<strong>Board. </strong>Once the players are chosen, the empty board is outputted first. Note that we always output two views of the board at the same time. The left view represents the current board state and the right one shows the board positions map (where the letters <em>a,b,c,…,p </em>denote the positions on the board) as shown in Figure 6 because the board is not rectangular. You do not need to worry about the board’s visualization because we have implemented the printing function in the provided code. Do not modify the printing function, or you will lose marks.

Figure 6: Empty board.

<strong>Every time </strong>a player does a <strong>legal </strong>movement on the board, the program will output the current state of the board.

<strong>Movements.        </strong>This program requires decisions of the following three operations from the human or computer players.

<ul>

 <li>PUT(<em>pos</em>): In Phase 1 of this game, the players put pieces in turn on the board. It takes an input of one letter as the position of the piece. If it is an illegal movement or input, the program will output a warning message “Invalid Put-Movement.” and request for input again. The input message’s format for players is like “Player 1 [Put] (pos): ” and it takes a input of one letter.</li>

 <li>MOVE(<em>s, t</em>): In Phase 2 of this game, the players move the existing pieces on the board and the input takes 2 letters: source position and target position. If it is an illegal movement or input, the program will output a warning message “Invalid Move-Movement.” and request for input again. The input message’s format for players is like “Player 1 [Move] (from to): ” and it takes an input of two letters separated by a space.</li>

 <li>REMOVE(<em>pos</em>): In either phase of the game, once a player forms a mill on the board, the player can do an <strong>extra </strong>movement, which removes an opponent’s piece. In this movement, it takes an input of one letter position. If it is an illegal removal or input, the program will output a warning message “Invalid Remove-Movement.” and request for input again. The input message’s format for players is like “Player 1 [Remove] (pos): ” and it takes a input of one letter.</li>

</ul>

A computer player always makes valid operations. The program should print out the input message of the corresponding operations and the decision by the computer player same as the message for human player.

<strong>Overall Interface. </strong>As shown in Figure 7, this is basically the whole interface of our game. The board will be displayed after <strong>every </strong>movement or play and each player has to make his decision for the requested movement. Although a computer player does not request for input, it outputs the decision in the same format as the human player does.

After the game ends, it will output a winning message for the winner like “Congratulation to the winner: Player 1!”.

<h2>2.3      Required Classes and Functions</h2>

To let you get familar with OO-design, we provide an OO class design framework for this game. You should follow this OO-design and must not modify the prototypes of any of these classes and functions. You can design extra functions if you find it necessary.

<h3>• class SixMensMorris</h3>

This class controls the overall game process, including phases 1 and 2 in Six Men’s Morris, and the starting and ending of the game.

<h3><strong>– </strong>board = Board()</h3>

This is a variable representing the game board.

<strong>– </strong>players = [Player(1), Player(2)]

This is an array with two variables representing the players.

<h4><strong>– </strong>num play = 0</h4>

This is a variable representing the number of total plays (one play denotes one movement by a player.). Each time a player does a movement, this variable is incremented by 1. We note that 1 round is equivalent to 2 plays.

<h4><strong>– </strong>next player(self)</h4>

This function returns the current player in this round.

Figure 7: The interface.

<h3><strong>– </strong>opponent(self, player)</h3>

This function returns the opponent of the player. If the argument is Player 1, then it will return Player 2, and vice versa.

<h3><strong>– </strong>check win(self, player)</h3>

This function returns a Boolean variable representing whether the player wins the game. It calls board.check win() in fact.

<strong>– </strong>start game(self)

This function controls the overall logic of the game.

<h3>• class Board</h3>

This class defines the game board and its properties such as the connected edges and all possible mills on the board, as well as a series of movements and legal movement checks on the board. The state of the board is controlled by the players.

<h4><strong>– </strong>state</h4>

This is the representation of the state of the game board, which stores an array of size 16.

<h4><strong>– </strong>mills</h4>

This variable pre-defines all possible mill configurations, each of which is represented as a 3-tuple on the board.

<h4><strong>– </strong>edges</h4>

This variable pre-defines all possible edges, each of which is represented as a 2-tuple on the board.

<h4><strong>– </strong>print board(self)</h4>

This function prints the current stored board state. It would print two views – one shows the board state and the other one shows the reference board positions for the players. Please refer to the visualization of the board in Figure 7.

<h3><strong>– </strong>check put(self, pos)</h3>

This function checks whether the PUT-movement is legal. The argument is the putting position. The output is a Boolean variable.

<h3><strong>– </strong>check move(self, s, t, player)</h3>

This function checks whether the MOVE-movement is legal. The arguments are the source position, the target position, and the player. The output is a Boolean variable.

<h3><strong>– </strong>check remove(self, pos, player)</h3>

This function checks whether the REMOVE-movement is legal for the player. The arguments are the position on which the piece is expected to be removed and the player. The output is a Boolean variable.

<ul>

 <li>put piece(self, pos, player)</li>

</ul>

This function does the PUT-movement on the board without checking.

<ul>

 <li>move piece(self, s, t, player)</li>

</ul>

This function does the MOVE-movement on the board without checking.

<ul>

 <li>remove piece(self, pos, player)</li>

</ul>

This function does the REMOVE-movement on the board without checking.

<h3><strong>– </strong>form mill(self, pos, player)</h3>

This function returns a Boolean variable representing whether it forms a mill at this position for the player.

<h3><strong>– </strong>check win(self, player, opponent)</h3>

This function returns a Boolean variable representing whether the current player wins. If the current player wins the game, then it returns True. Otherwise, it returns False. Please refer to the winning conditions.

<h3>• class Player</h3>

This class defines the behaviors of players. The player can put pieces, move pieces and remove pieces on the board.

<ul>

 <li>id</li>

</ul>

Player’s id. It is an integer 0 or 1.

<ul>

 <li>symbol</li>

</ul>

Player’s symbol. Player 1 uses “#” but Player 2 uses “@”.

<ul>

 <li>board</li>

</ul>

This is the game board for the player.

<h4><strong>– </strong>next put(self)</h4>

This function defines a PUT-movement for the player. It should be implemented by the Human and Computer classes. <strong>It returns the position to which the piece is put because it might trigger the formation of a mill.</strong>

<h4><strong>– </strong>next move(self)</h4>

This function defines a MOVE-movement for the player. It should be implemented by the Human and Computer classes. <strong>It returns the position to which the piece moves because it might trigger the formation of a mill.</strong>

<strong>– </strong>next remove(self, opponent) This function defines a REMOVE-movement for the player. It should be implemented by the Human and Computer classes.

<h3>• class Human</h3>

This class extends the superclass Player to play the game, where the player’s movements are from the input of the user.

<h4><strong>– </strong>next put(self)</h4>

This function outputs a prompt and takes a single location input for a PUT-movement. Specifically, the input message’s format is like “Player 1 [Put] (pos): ” and it takes an input of one letter. It keeps checking whether it is a legal PUT-movement until the input is legal. After getting the correct input, it then does the movement on the board (by calling board.put piece()). <strong>It returns the position where the piece to put because it might trigger the formation of a mill. </strong>When there is an error input, it will output a warning message “Invalid Put-Movement.”.

<h4><strong>– </strong>next move(self)</h4>

This function outputs a prompt and takes two location inputs (s, t) for a MOVEmovement. Specifically, the input message’s format for players is like “Player 1 [Move] (from to): ” and it takes an input of two letters separated by a space. It keeps checking whether it is a legal MOVE-movement until the input is legal. After getting the correct input, it then does the movement on the board (by calling board.move piece()). <strong>It returns the position to which the piece moves because it might trigger the formation of a mill. </strong>When there is an error input, it will output a warning message “Invalid Move-Movement.”.

<h3><strong>– </strong>next remove(self, opponent)</h3>

This function outputs a prompt and takes a location input for a REMOVE-movement. Specifically, The input message’s format for players is like “Player 1 [Remove] (pos): ” and it takes a input of one letter. It keeps checking whether it is a legal REMOVEmovement until the input is legal. After getting the correct input, it then does REMOVEmovement on the board (by calling board.remove piece()). It returns nothing. When there is an error input, it will output a warning message “Invalid Remove-Movement.”.

<h3>• class Computer</h3>

This class extends the superclass Player to play the game, where the player’s movement is generated by the computer.

<h4><strong>– </strong>next put(self)</h4>

This function randomly generates a legal PUT-movement and does the movement on the board (by calling board.put piece()). It outputs the same message like “Player 1 [Put] (pos): ” and one letter representing his decision. <strong>It returns the position where the piece locates because it might trigger the formation of a mill. </strong>Note that the computer only generates a legal movement and thus print no warning message.

<h4><strong>– </strong>next move(self)</h4>

This function randomly generates a legal MOVE-movement (s,t) and then does the movement on the board (by calling board.move piece()). It outputs the same message as the human player: “Player 1 [Move] (from to): ” and two letters representing his decision. <strong>It returns the position to which the piece moves because it might trigger the formation of a mill. </strong>Note that the computer only generates a legal movement and thus print no warning message.

<h3><strong>– </strong>next remove(self, opponent)</h3>

This function randomly generates a legal REMOVE-movement and does REMOVEmovement on the board (by calling board.remove piece()). It outputs the same message like “Player 1 [REMOVE] (pos): ” and one letter representing his decision. It returns nothing. Note that the computer only generates a legal movement and thus print no warning message.

<h2>2.4      Your programming task</h2>

Overall there are six source files, one for each defined class and additional tools file: Board.py, Computer.py, Human.py, Player.py, SixMensMorris.py, utils.py. The files are templates. Your task is to <strong>complete the missing parts of the code which are marked by “TODO”</strong>. The programming environment is Python3 (Python3.5+) only.

<ol>

 <li>Complete your name and student ID in every file.</li>

 <li>Based on the above problem specification, complete the game program by implementing the above member functions.</li>

 <li>The program starts by running “python3 SixMensMorris.py”. You should design enough corner cases to test your program.</li>

</ol>

Things to note:

<ol>

 <li>Apart from completing these member functions, <strong>Do Not </strong>change any other parts of our provided source code.</li>

 <li>Please strictly follow the Input/Output specification in Subsection 2.2.2. You might easily get the I/O details by directly going through the provided code. Otherwise, your marks can be deducted.</li>

 <li>For better visualization, we added color in the output and you can find the color functions in the file “utils.py”. You should not change the color or its uses in the source code. Otherwise, it might cause errors when we are comparing the output content by machines.</li>

 <li>In Python, there is a library that you can use to debug the code, <em>e.</em>, ipython. You can simply insert “from IPython import embed; embed()” and run the program. Then you can debug your program like checking the variable values or debugging the code you write while the code is running.</li>

</ol>

<h1>3          Task 2: Demonstrating Advantages and Disadvantages of Dynamic Typing</h1>

These are commonly-claimed advantages and disadvantages of Dynamic Typing:

<ol>

 <li>Advantages

  <ul>

   <li>More generic code can be written. In other words, functions can be defined to apply on arguments of different types.</li>

   <li>Possibilities of mixed type collection data structures.</li>

  </ul></li>

 <li>Disadvantage

  <ul>

   <li>Loss of type checking at compile time.</li>

  </ul></li>

</ol>

Please provide concise example codes <em>designed by yourself or extracted from any code you write for this assignment </em>to demonstrate the advantages and disadvantage of Dynamic Typing mentioned above. You are welcome to provide other advantages or disadvantages along with code fragment for extra bonus points.

<h1>4         Task 3: Save The Tribe</h1>

This task is to build a game in Python. A Java implementation of the game is given. You need to understand its behavior and re-implement it with Python. After finishing this task, you will have experienced a special feature of Python called Duck Typing, which is possible only in a dynamically typed language. And you will see a difference between the Java and Python implementations, the former of which does not support Duck Typing.

<h2>4.1      Duck Typing</h2>

The following synopsis of Duck Typing is summarized from:

<a href="https://en.wikipedia.org/wiki/Duck%20typing">http://en.wikipedia.org/wiki/Ducktyping</a>

<a href="http://www.sitepoint.com/making-ruby-quack-why-we-love-duck-typing">http://www.sitepoint.com/making-ruby-quack-why-we-love-duck-typing</a>

In standard statically-typed object-oriented languages, objects’ classes (which determine an object characteristics and behavior) are essentially interpreted as the objects’ types. Duck Typing is a new typing paradigm in dynamically-typed (late binding) languages that allows us to dissociate typing from objects’ characteristics. It can be summarized by the following motto by the late poet James Whitcombe Riley:

When I see a bird that walks like a duck and swims like a duck and quacks like a duck, I call that bird a duck.

The basic premise of Duck Typing is simple. If an entity looks, walks, and quacks like a duck, for all intents and purposes it is fair to assume that one is dealing with a member of the species anas platyrhynchos. In practical Python terms, this means that it is possible to try calling any method on any object, regardless of its class.

An important advantage of Duck Typing is that we can enjoy <em>polymorphism without inheritance</em>. An immediate consequence is that we can write more generic codes, which are cleaner and more concise.

<h2>4.2     Background</h2>

In Ancient Rome, a tribe is attacked by alien invaders. The only way to wipe out these invaders is to seek an artifact from a desert nearby. However, the desert is very dangerous with many monsters residing there.

With the mission to save the tribe, a soldier (the player) comes to the desert and starts his journey to seek the artifact. Each monster in the desert lives in its own cave and the artifact is taken by one of the monsters. The soldier has to enter the cave and kill the monster in a topological order so that (s)he could get the keys to enter other caves. Figure 8 illustrates the pre-defined topological order, where each node represents a cave. If the soldier wants to enter cave 2, (s)he has to kill the monster inside cave 5 or cave 1 first to get the key for cave 2. The monster inside cave 7 keeps the artifact that the soldier wants to collect.

Figure 8: Topological order to kill the monsters.

<h2>4.3     Task Description</h2>

At the beginning, there are 7 monsters and a spring in the desert. All of them are distributed in different positions, as illustrated in Figure 9. The health capacity of the soldier is 100, the health capacity of the monsters is a random number in the range of 30–70, which must be in multiples of 10. The soldier can drink the spring water to recover fully his health. Before exploring the desert, the soldier is equipped with 2 elixirs to increase his health during fight, as well as the keys to enter cave 5 and cave 1.

Figure 9: Map of the desert. Symbols of <em>M</em>, <em>S </em>and @ represent the monsters, soldier and spring respectively.

<ul>

 <li>At each iteration, the soldier can move to the next grid cell in the desert.</li>

</ul>

− When meeting a cave, the monster inside will check whether the soldier has the key to enter or not.

<ul>

 <li>If yes, the soldier will fight with the monster in a round-based manner. In each round, the soldier has three options:

  <ol>

   <li>Attack: The health of the monster will be damaged by 10. If the monster is still alive, the health of the soldier will also be damaged by 10. Enter next round. <em>Note that the soldier always attacks first.</em></li>

   <li>Escape: The soldier escapes and the health of monster will be recovered to its health capacity automatically. The fight is over.</li>

   <li>Use Elixir: The soldier uses elixir, which could increase her/his health by 15 to 20 randomly. Enter next round.</li>

  </ol></li>

</ul>

If the soldier successfully kills the monster (health of monster is reduced to 0 or less), (s)he will get the dropped item(s) from the monster. Otherwise, when the health of the soldier is reduced to 0 or less, the soldier is dead and the game is over.

<ul>

 <li>If no, the monster will tell the soldier where (s)he can collect the key to enter this cave.</li>

</ul>

− When meeting the spring, the soldier will drink the water and recover his health to 100.

The soldier can only the water for one time.

<ul>

 <li>When the soldier gets the artifact from the monsters, the game will be over.</li>

</ul>

You should read and execute the given Java program to understand its behavior and design. Then please replicate all the behavior of the given Java Program in Python with Duck Typing, following the same class design. You should not introduce extra instance variables or instance methods. You program should run by calling python3 SaveTheTribe.py. You will also be evaluated on your programming style.

<h1>5         Task 4: Strengthen Yourself</h1>

A merchant comes to the desert. The soldier could buy shield or elixir with coins to strengthen himself, which enables him to kill the monster more easily. After killing each monster, the soldier could get one coin.

<h2>5.1      New Game Elements</h2>

At the beginning, there are 7 monsters (<em>M</em>), a merchant ($), and a spring (@) in the desert. The merchant is located at (7,7) on the map. Note that the soldier has no coins initially.

<ul>

 <li>At each iteration, the soldier can move to the next grid cell in the desert.</li>

</ul>

− When meeting a cave, the monster inside will check whether the soldier has the key to enter or not.

<ul>

 <li>If yes, the soldier will fight with the monster in a round-based manner. In each round, the soldier has three options:

  <ol>

   <li>Attack: The health of the monster will be damaged by 10. If the monster is still alive, the health of the soldier will also be damaged by 10 – his defence value, but the damage value is no less than zero. Enter next round. <em>Note that the soldier always attacks first.</em></li>

   <li>Escape: The soldier escapes and the health of monster will be recovered to its health capacity automatically. The fight is over.</li>

   <li>Use Elixir: The soldier uses elixir, which could increase her/his health by 15 to 20 randomly. Enter next round.</li>

  </ol></li>

</ul>

If the soldier successfully kills the monster (health of monster is reduced to 0 or less), he will get the dropped item(s) and one coin from the monster. Otherwise, when the health of the soldier is reduced to 0 or less, he is defeated and will escape automatically.

<ul>

 <li>If no, the monster will tell the soldier where (s)he can collect the key to enter this cave.</li>

</ul>

− When meeting the spring, the soldier will drink the water and recover his health to 100.

− When meeting the merchant, the soldier can buy a shield with two coins, or an elixir with one coin. Each shield can improve the defence value of the soldier by 5.

<ul>

 <li>When the soldier gets the artifact from the monsters, the game will be over.</li>

</ul>

<h2>5.2      Program Enhancement</h2>

You are now required to enhance both the Java and Python implementations of Task 3, according to the requirements below:

<ol>

 <li>You need to add a <strong>Merchant </strong> A Java template is provided for your reference.</li>

 <li>You need to make appropriate modifications to the <strong>Soldier </strong>and <strong>Monster </strong>classes, for which you need to use the power of inheritance as much as possible. For example, for the modification of the <strong>Soldier </strong>class, you need to <em>add a subclass </em>of the <strong>Soldier </strong>class, and name it as <strong>Task4Soldier </strong>class, instead of modifying the <strong>Soldier </strong>class directly.</li>

 <li>You need to make appropriate modifications to the <strong>SaveTheTribe </strong>and <strong>Map </strong>classes in Java, but only need to modify <strong>SaveTheTribe </strong>class in Python, due to the usage of Duck Typing. For the changes on these two classes, you are allowed to modify the original class design of Task 3.</li>

 <li>You are required to name each class that you have modified or added for Task 4 as <strong>Task4xxx</strong>. For example, if you modify the <strong>SaveTheTribe </strong>class, please name it as <strong>Task4SaveTheTribe</strong>, and name the corresponding file as Task4SaveTheTribe.py or Task4SaveTheTribe.java.</li>

 <li>You are required to display all the attributes of the soldier in each iteration, as illustrated in Figure 10.</li>

 <li>Your program should be run by calling python3 Task4SaveTheTribe.py and javac Task4SaveTheTribe.java.</li>

</ol>

Figure 10: Displayed information in each iteration.

<h1>6      Report</h1>

Your simple report should answer the following questions within TWO A4 pages.

<ol>

 <li>Providing example code and necessary elaborations for demonstrating advantages and disadvantages of Dynamic Typing as specified in Task 2.</li>

 <li>Using codes for Task 3, give two scenarios in which the Python implementation is better than the Java implementation. Given reasons.</li>

</ol>

Using codes for Task 4, illustrate further advantages of Duck Typing