Download Link: https://assignmentchef.com/product/solved-bbm104-assignment-3-polymorphism-exceptions
<br>
In this experiment, you are expected to implement an application which is the logic core simulator of a simple board game. Main focus point of this experiment is to get you familiar with polymorphism. Implementing the program without using the benefits of polymorphism will be penalized.

<h1>2           Problem</h1>

There are two sides which are called Zorde and Calliance. Main theme of the game is the war between two sides. Each side has 3 different types of characters. The game is played on a board where each character occupies a cell on the board (just like chess). During the progress of the game, each side makes moves in turns. The aim of the game is to kill every opponent character.

<h2>2.1         Hit Point</h2>

Each character has a hit point (HP) value which indicates how healthy they are. This value is lowered equally to the damage taken when a character is being attacked by another character. If a character’s HP value is 0 or below, they are considered dead.

<h2>2.2         Attack Power</h2>

Attack power (AP) of a character indicates how hard it can attack its opponents. This value determines how much damage will be taken by the defending character. By default, damage done by an attacking character is equal to its AP so when it attacks another character, this value will be subtracted from the defender’s HP.

The table below shows cell types of each side and their default (initial) HP and AP values.

<h2>2.3         Board and Initial Armies</h2>

The game takes place on a board which is very similar to a chess board. Size of the board and initial armies of both sides (including their initial positions) will be provided via an input file, the initials file.

During the game, you will create an output showing the current status of the board. In the output, the board should be formatted exactly as shown in the figure below (a). Note that there is one line for each row (horizontally) and two character spaces for each column

(vertically) (b).

<h2>2.4         Commands</h2>

The program you will implement is a turn based strategy game, therefore, the players will make their moves in turns as the game continues. The moves made by each player is supplied via an input file, the <em>commands file</em>. Each line of the commands file indicates a single move made by a player.

As you can see in the figure, a move command starts with the ID of the character to be moved, which is followed by a sequence of integers that are inside the interval [-1, 1] (i.e. the sequence may only contain -1, 0 and 1) and these integer numbers are separated by semicolons. This sequence consists of even number of integer as each couple indicates one step of the move. For example, at the first line of the figure the integer sequence indicates a 4 step move as illustrated in the figure. If we look at the position of E0, its current position is at the position of “4 8”, and if we make a move step with 0;-1, then its position will shift to the “4 7” on the board.

After reading the initials file and locating the characters on the game board, your program should start reading the commands file line by line and execute the moves of the players. The program should exit when it reaches the end of the commands file.

<h2>2.5         Output</h2>

After execution of each line of the commands file, your program should create and output which shows the current status of the board (i.e. positions of the characters) and their current and default HP values as shown in the figure. Please note that the list below the board is ordered by the character IDs. You can use the ’tab’ character (i.e. ) between line tokens so that the output will look aligned vertically. Please do not forget to create an initial output right after reading from the initials file and before starting to execute the commands.

<em>P.S. Representation of sample I/O is given in Appendix (Section 9).</em>

<h1>3           Details about Moves of the Characters and Attacking</h1>

At the tables below, you can find the move types of each character type. Move types also determine when a character attacks. When a character makes an attack, it attacks to all of the 8 cells around its current position. While some characters make an attack after each step of their move (i.e. if the character makes 4 steps, it attacks 4 times, after each step), some characters can only make an attack after their final step (i.e. if the character makes 4 steps,

<table width="593">

 <tbody>

  <tr>

   <td width="96"><strong>ZORDE</strong></td>

   <td width="176"> </td>

   <td width="176"> </td>

   <td width="144"> </td>

  </tr>

  <tr>

   <td width="96"> </td>

   <td width="176"><strong>Ork</strong></td>

   <td width="176"><strong>Troll</strong></td>

   <td width="144"><strong>Goblin</strong></td>

  </tr>

  <tr>

   <td width="96"><strong>Move steps</strong></td>

   <td width="176">1</td>

   <td width="176">1</td>

   <td width="144">4</td>

  </tr>

  <tr>

   <td width="96"><strong>Attack type</strong></td>

   <td width="176">Attacks after the final step.</td>

   <td width="176">Attacks after the final step.</td>

   <td width="144">Attacks at every step.</td>

  </tr>

  <tr>

   <td width="96"><strong>Special</strong></td>

   <td width="176">Heals friendly neighbors (10) before every move sequence (not move step).</td>

   <td width="176">N/A</td>

   <td width="144">N/A</td>

  </tr>

  <tr>

   <td colspan="2" width="272"><strong>CALLIANCE</strong></td>

   <td width="176"> </td>

   <td width="144"> </td>

  </tr>

  <tr>

   <td width="96"> </td>

   <td width="176"><strong>Human</strong></td>

   <td width="176"><strong>Elf</strong></td>

   <td width="144"><strong>Dwarf</strong></td>

  </tr>

  <tr>

   <td width="96"><strong>Move steps</strong></td>

   <td width="176">3</td>

   <td width="176">4</td>

   <td width="144">2</td>

  </tr>

  <tr>

   <td width="96"><strong>Attack type</strong></td>

   <td width="176">Attacks after the final step.</td>

   <td width="176">Attacks at every step.</td>

   <td width="144">Attacks at every step.</td>

  </tr>

  <tr>

   <td width="96"><strong>Special</strong></td>

   <td width="176">N/A</td>

   <td width="176">Makes a ranged attack(instead of the final attack) after every move sequence (not move step). AP:15, range:2</td>

   <td width="144">N/A</td>

  </tr>

 </tbody>

</table>

it attacks only once after the final step).

As explained above (see the attack power section), attacking means, decreasing an defender’s HP value by the amount of the attacker’s AP value.

<h2>3.1         COMBAT RULES</h2>

<ol>

 <li>Characters cannot move onto the friendly characters (friendly character means characters that are at the same side). If a character tries to move onto a friendly character, its move is finalized at the current location and the rest of its move sequence will be ignored. For example if a character tries to move onto a friendly character at the second step of a 4-step move, only the first step of the move will be executed.</li>

 <li>Characters can move onto the enemy characters. If such a situation occurs, two enemy characters that are at the same cell fight to the death for the cell. Before a fight to the death, the attacking character will make a single attack to the defending character with its attack power. A fight to the death can be won by the character that has the highest current HP value but its HP value will decrease by an amount equal to the losing characters current HP value. For example, if a human (current HP : 100) moves onto a cell that is currently occupied by an ork (current HP : 60), the human will make an initial attack to the ork (now, the ork’s current HP is 30). Then, the ork will die and human’s HP value will decrease to 70.

  <ul>

   <li>The attack that is made before the fight to the death is not a normal attack. Thus, it will only effect the defending enemy character, not the other characters at the neighboring 8 cells.</li>

   <li>After a fight to the death, the attacker will stop moving. For example if a character tries to move onto an enemy character at the second step of a 4-step move, even if the attacker is the winner of the fight to the death, only the first and second steps of the move will be executed. The rest of the move sequence will be ignored.</li>

   <li>If two characters have same HP just before a fight to the death, they both die.</li>

  </ul></li>

 <li>Before they start a move sequence, Orks will first heal any friendly character in one of the neighboring cells.

  <ul>

   <li>Friendly characters will be healed by 10 hit points.</li>

   <li>A character’s hit point cannot exceed its default hit point via healing. If this happens, you should decrease the current hit point to the default hit point of that character.</li>

   <li>When healing the neighboring characters, Orks will heal themselves too.</li>

  </ul></li>

 <li>After they finish a move sequence, Elfs will make a ranged attack (instead of the final step’s default attack) to all enemy characters that are in range of 2 cells with an attack power of 15.

  <ul>

   <li>If an Elf’s move sequence is interrupted by moving through an enemy character, then this power cannot be used. This power can only be used if the Elf completes its whole move sequence without being interrupted.</li>

  </ul></li>

 <li>Game ends when all characters of one side is dead. When the game ends, you should add a line indicating the winner of the game as shown in the figure.</li>

</ol>

<h1>4           Error Handling</h1>

You will need to check for only 2 errors by creating custom exceptions. All the input files will be error free apart from these controls :

<ol>

 <li>Boundary Check: You need to check if a move in the move sequence exceeds the boundaries of the game board. If it does, you should print an error message such as:</li>

</ol>

“Error : Game board boundaries are exceeded. Input line ignored.” And you should also ignore the input line completely.

<ol start="2">

 <li>Move Count Check: You need to check if a move sequence in the commands file has exact number of move steps according to the character types. If there are more or less move steps etc., you should print an error message such as:</li>

</ol>

”Error : Move sequence contains wrong number of move steps. Input line ignored.” You should not need to check anything other than these two error situations.

<h1>5           Design Notes</h1>

<ul>

 <li>Class that contains your main method should be named ”Main.java”.</li>

 <li>Some default values are given to you in this document, such as AP values, you will also be supplied a class file named “Constants.java”. You can find this file via Piazza. This is a JAVA class called Constants and contains variables corresponding to some values given in this document. You have to use the variables from this file while implementing your software. Do not hard-code these values into your code. The variables in the file are defined as public variables so you can easily use them anywhere in your project. Download this file and put it into your project before you start coding. And don’t forget to use it!!!</li>

 <li>The files specified in the pdf are going to be given as program arguments. There will be text files (initials.txt, commands.txt) in your working directory. The input and output files will be given as program arguments from the command line. In order to test your program, you should follow the following steps:

  <ul>

   <li>Upload your java files to your server account (dev.cs.hacettepe.edu.tr)</li>

   <li>Compile your code (javac *.java)</li>

   <li>Run your program (java Main initials.txt commands.txt output.txt)</li>

   <li>Control your output data (output.txt).</li>

  </ul></li>

 <li>Samples of input and output files can be found on Piazza. Examine them carefully during coding.</li>

</ul>

<h2>5.1         Report</h2>

Your final report should contain these topics:

<ol>

 <li>Cover Page</li>

 <li>Software Design Notes Problem: Re-define the experiment in your own words. Keep the definition short by mentioning only the important parts. DO NOT COPY PASTE FROM THIS DOCUMENT.</li>

</ol>

<ul>

 <li>Solution:

  <ul>

   <li>Explain how you approached the problem, what was the most important part of the problem from your perspective and how it effected your design. And then add anything else that you thing will further explain your design.</li>

   <li>Provide a class diagram at the solution section. Below the diagram, give an explanation for each class’s role in the design. Use only 1 – 2 sentences for each class. If you have more to say, you should say it at the first part of the solution section. If your class diagram is too big to be put in the report file, submit it as a jpg file with the report.</li>

  </ul></li>

</ul>