Download Link: https://assignmentchef.com/product/solved-csci-1133-assignment-11-rpg-fight
<br>
You are designing a text-based <u><a href="https://en.wikipedia.org/wiki/Role-playing_game">Role</a><a href="https://en.wikipedia.org/wiki/Role-playing_game">–</a><a href="https://en.wikipedia.org/wiki/Role-playing_game">Playing Game</a></u> (RPG), in which each character can have one of three jobs: Fighter, Thief, or Wizard.  You need a way to keep track of the data for each character, and because a lot of the data and functionality is shared between characters, you have decided to use objects and inheritance to accomplish this.

<strong>Part 1: </strong>

First, you’ll need a base Adventurer class, which represents a jobless character template for all of the job classes to build off of.

The Adventurer class should have the following methods:




<ul>

 <li>Constructor: The Adventurer class constructor should have the following signature:</li>

</ul>




<h1>__init__(self, name, level, strength, speed, power)</h1>




where name (the name of the Adventurer) should be a string, and level, strength, speed, and power should be integers that represent the Adventurer’s ability levels.  The constructor should create instance variables to store the value of each of these arguments (self.name, self.level, self.strength, self.speed, and self.power, respectively), along with two more instance variables:




<ul>

 <li>HP, an integer representing the Adventurer’s remaining Hit Points, which should be initialized to the Adventurer’s level multiplied by 6.</li>

 <li>hidden, a boolean representing whether the Adventurer is currently hiding, which should be initialized to False.</li>

</ul>




<h1>● __repr__(self)</h1>




You must overload the repr() method (similar to the str() method, except that it also changes what is output when you pass the object directly to the interpreter) for the Adventurer class so that it returns a string of the format:




“&lt;Name&gt; – HP: &lt;Current HP&gt;”




Be sure to match the spacing and format of the above string exactly or you will fail test cases and lose points (note that the angled brackets are <u>not</u> part of the string itself, but indicate where you should substitute in the actual name and hit points of your adventurer).  Note that changing __repr__ automatically changes the behavior of str() as well.  See the sample output below for an example.




<h1>● attack(self,target)</h1>




The attack method takes as a parameter another Adventurer object target and does the following:




<ul>

 <li>If the target is hidden, then this method should print the string:</li>

</ul>




“&lt;Name&gt; can’t see &lt;Target’s name&gt;”

<ul>

 <li>Otherwise, this method should the compute the damage the Adventurer does (their strength + 4), and subtract that value from the target’s HP. The method should update target’s hit points accordingly, and print out a message of the following format:</li>

</ul>




“&lt;Name&gt; attacks &lt;Target’s name&gt; for &lt;Damage amount&gt; damage”




Example: (<em>italic text</em> is printed, <strong>bold text</strong> is returned)




&gt;&gt;&gt; thog = Adventurer(“Thog”,3,5,1,2)

&gt;&gt;&gt; repr(thog)

<h2>‘Thog – HP: 18’</h2>

&gt;&gt;&gt; goku = Adventurer(“Goku”,20,10,7,9001)

&gt;&gt;&gt; goku

Goku – HP: 120

&gt;&gt;&gt; thog.attack(goku)

<em>Thog attacks Goku for 9 damage </em>

&gt;&gt;&gt; str(goku)

<h2>‘Goku – HP: 111’</h2>

&gt;&gt;&gt; goku.HP

111

&gt;&gt;&gt; goku.hidden = True

&gt;&gt;&gt; thog.attack(goku)

<em>Thog can’t see Goku </em>

&gt;&gt;&gt; goku.attack(thog)

<em>Goku attacks Thog for 14 damage </em>

&gt;&gt;&gt; print(thog)

<em>Thog – HP: 4 </em>

&gt;&gt;&gt; goku.attack(thog)

<em>Goku attacks Thog for 14 damage </em>

&gt;&gt;&gt; thog.HP

-10




<strong>Part 2: </strong>

Construct three additional classes named Fighter, Thief, and Wizard to represent each of the three possible specializations for an Adventurer.  Each of these classes should inherit from the Adventurer class and extend it by overloading the constructor and attack methods.




Fighter:




<ul>

 <li>The Fighter constructor must take the same parameters as its superclass constructor and pass them into the superclass constructor, and must then alter HP to be initialized to level * 12 rather than level * 6.</li>

 <li>The overridden attack method for Fighter is identical to that of Adventurer except that a</li>

</ul>

Fighter does (2*strength + 6) damage to enemies that aren’t hidden rather than (strength + 4).




Thief:




<ul>

 <li>The Thief constructor must take the same parameters as its superclass constructor and pass them into the superclass constructor, and must then alter HP to be initialized to level * 8 rather than level * 6, and set self.hidden to True.</li>

 <li>The overridden attack method for Thief should call the superclass method of the same name in the case that the Thief is not hidden (that is, when hidden is False). If the Thief is hidden, then instead the following should occur:

  <ul>

   <li>If both the Thief and the target are hidden, and the Thief’s speed is less than the target’s speed, then the Thief is unable to find their target and the method should print a message of the format:</li>

  </ul></li>

</ul>




“&lt;Name&gt; can’t see &lt;Target’s name&gt;”




○ Otherwise, the Thief is able to perform a sneak attack.  This does damage equal to (speed + level) * 5.  It also causes the Thief and their target (if applicable) to no longer be hidden, and should print a message of the format:




“&lt;Name&gt; sneak attacks &lt;Target’s name&gt; for &lt;Damage amount&gt; damage”




Wizard:




<ul>

 <li>The Wizard constructor must take the same parameters as its superclass constructor and pass them into the superclass constructor, and must then initialize a new instance variable,</li>

</ul>

self.fireballs_left, initially equal to the Wizard’s power.

<ul>

 <li>The overridden attack method for Wizard should call the superclass method of the same name in the case that the Wizard has no fireballs left (that is, fireballs_left is 0).</li>

</ul>

If the Wizard does have fireballs left, the Wizard should instead cast a fireball:

<ul>

 <li>A fireball causes the target to no longer be hidden (if applicable), and does (level * 3) damage to the target. Remember to subtract one from the Wizard’s number of fireballs left.  Casting a fireball should also print a message of the format:</li>

</ul>




“&lt;Name&gt; casts fireball on &lt;Target’s name&gt; for &lt;Damage amt&gt; damage”

<strong> </strong>

<strong>Part 3: </strong>

Finally, create a function (not part of any class) called duel(adv1, adv2) which takes two Adventurer objects adv1 and adv2 as parameters and returns True if adv1 would win in a one-onone fight, or False otherwise.  Specifically, the function should do the following:




<ul>

 <li>If at any point adv1 reaches 0 or fewer HP while adv2 still has more than 0 HP, duel should print out adv1 and adv2, followed by a message of the form:</li>

</ul>

“&lt;adv2’s name&gt; wins!”

and then return False.




<ul>

 <li>If at any point adv2 reaches 0 or fewer HP while adv1 still has more than 0 HP, duel should print out adv1 and adv2, followed by a message of the form:</li>

</ul>

“&lt;adv1’s name&gt; wins!”

and then return True.




<ul>

 <li>If adv1 and adv2 somehow reach 0 HP or below simultaneously (because they start the duel like that, or because they’re the same object) duel should print out adv1 and adv2, followed by the message:</li>

</ul>

“Everyone loses!”

and then return False.




<ul>

 <li>Otherwise, the duel should proceed: adv1 and adv2 should be printed out to see the current HP counts, then adv1 should attack adv2, and then adv2 should attack adv1. This should repeat until one of the above conditions is met.</li>

</ul>




<ul>

 <li>Remember, you must check whether one or both Adventurers is at 0 or fewer HP after EVERY attack, not just every pair of attacks: if adv2 reaches 0 or fewer HP after adv1 attacks, then adv2 should not get a chance to retaliate.</li>

</ul>




<strong>Constraints</strong>:

<ul>

 <li>Your file should only contain class definitions and the duel No code should be included outside of the classes/function (though, as usual, comments are fine).</li>

 <li>You must name all classes, methods, and instance variables EXACTLY as specified.</li>

 <li>You should not import any modules.</li>

</ul>




Examples: (<em>italic text</em> is printed, <strong>bold text</strong> is returned)




Example 1:




&gt;&gt;&gt; albus = Wizard(“Dumbledore”,15,4,6,2)

&gt;&gt;&gt; smeagol = Thief(“Gollum”,12,1,4,1)

&gt;&gt;&gt; bruce = Thief(“Batman”,10,4,5,1)

&gt;&gt;&gt; duel(albus,smeagol)

<em>Dumbledore – HP: 90 </em>

<em>Gollum – HP: 96 </em>

<em>Dumbledore casts fireball on Gollum for 45 damage </em>

<em>Gollum attacks Dumbledore for 5 damage </em>

<em>Dumbledore – HP: 85 </em>

<em>Gollum – HP: 51 </em>

<em>Dumbledore casts fireball on Gollum for 45 damage </em>

<em>Gollum attacks Dumbledore for 5 damage </em>

<em>Dumbledore – HP: 80 </em>

<em>Gollum – HP: 6 </em>

<em>Dumbledore attacks Gollum for 8 damage </em>

<em>Dumbledore – HP: 80 </em>

<em>Gollum – HP: -2 </em>

<em>Dumbledore wins! </em>

<h2>True</h2>

&gt;&gt;&gt; duel(bruce,albus)

<em>Batman – HP: 80 </em>

<em>Dumbledore – HP: 80 </em>

<em>Batman sneak attacks Dumbledore for 75 damage </em>

<em>Dumbledore attacks Batman for 8 damage </em>

<em>Batman – HP: 72 </em>

<em>Dumbledore – HP: 5 </em>

<em>Batman attacks Dumbledore for 8 damage </em>

<em>Batman – HP: 72 </em>

<em>Dumbledore – HP: -3 </em>

<em>Batman wins! </em>

<h2>True</h2>

<strong> </strong>

Example 2:

<strong> </strong>

&gt;&gt;&gt; durden = Fighter(“Tyler”,6,3,2,1)

&gt;&gt;&gt; duel(durden,durden)

<em>Tyler – HP: 72 </em>

<em>Tyler – HP: 72 </em>

<em>Tyler attacks Tyler for 12 damage </em>

<em>Tyler attacks Tyler for 12 damage </em>

<em>Tyler – HP: 48 </em>

<em>Tyler – HP: 48 </em>

<em>Tyler attacks Tyler for 12 damage </em>

<em>Tyler attacks Tyler for 12 damage </em>

<em>Tyler – HP: 24 </em>

<em>Tyler – HP: 24 </em>

<em>Tyler attacks Tyler for 12 damage </em>

<em>Tyler attacks Tyler for 12 damage </em>

<em>Tyler – HP: 0 </em>

<em>Tyler – HP: 0 </em>

<em>Everyone loses! </em>

<h2>False</h2>




Example 3:




&gt;&gt;&gt; jack = Thief(“Jack”,7,2,5,1)

&gt;&gt;&gt; will = Thief(“Will”,8,3,4,2)

&gt;&gt;&gt; elizabeth = Thief(“Elizabeth”,5,3,3,2)

&gt;&gt;&gt; duel(will,jack)

<em>Will – HP: 64 </em>

<em>Jack – HP: 56 </em>

<em>Will can’t see Jack </em>

<em>Jack sneak attacks Will for 60 damage </em>

<em>Will – HP: 4 </em>

<em>Jack – HP: 56 </em>

<em>Will attacks Jack for 7 damage </em>

<em>Jack attacks Will for 6 damage </em>

<em>Will – HP: -2 </em>

<em>Jack – HP: 49 </em>

<em>Jack wins! </em>

<h2>False</h2>

&gt;&gt;&gt; duel(jack,will)

<em>Jack – HP: 49 </em>

<em>Will – HP: -2 </em>

<em>Jack wins! </em>

<h2>True</h2>

&gt;&gt;&gt; jack.hidden

False

&gt;&gt;&gt; elizabeth.hidden

True

&gt;&gt;&gt; duel(jack,elizabeth)

<em>Jack – HP: 49 </em>

<em>Elizabeth – HP: 40 </em>

<em>Jack can’t see Elizabeth </em>

<em>Elizabeth sneak attacks Jack for 40 damage </em>

<em>Jack – HP: 9 </em>

<em>Elizabeth – HP: 40 </em>

<em>Jack attacks Elizabeth for 6 damage </em>

<em>Elizabeth attacks Jack for 7 damage </em>

<em>Jack – HP: 2 </em>

<em>Elizabeth – HP: 34 </em>

<em>Jack attacks Elizabeth for 6 damage </em>

<em>Elizabeth attacks Jack for 7 damage </em>

<em>Jack – HP: -5 </em>

<em>Elizabeth – HP: 28 </em>

<em>Elizabeth wins! </em>

<h2>False</h2>

Example 4:




&gt;&gt;&gt; sean_bean = Fighter(“Boromir”,5,5,3,1)

&gt;&gt;&gt; orc1 = Fighter(“Orc”,1,5,1,1)

&gt;&gt;&gt; orc2 = Fighter(“Orc”,1,5,1,1)

&gt;&gt;&gt; orc3 = Fighter(“Orc”,1,5,1,1)

&gt;&gt;&gt; orc4 = Fighter(“Orc”,1,5,1,1)

&gt;&gt;&gt; duel(orc1,sean_bean)

<em>Orc – HP: 12 </em>

<em>Boromir – HP: 60 </em>

<em>Orc attacks Boromir for 16 damage </em>

<em>Boromir attacks Orc for 16 damage </em>

<em>Orc – HP: -4 </em>

<em>Boromir – HP: 44 </em>

<em>Boromir wins! </em>

<h2>False</h2>

&gt;&gt;&gt; duel(orc2,sean_bean)

<em>Orc – HP: 12 </em>

<em>Boromir – HP: 44 </em>

<em>Orc attacks Boromir for 16 damage </em>

<em>Boromir attacks Orc for 16 damage </em>

<em>Orc – HP: -4 </em>

<em>Boromir – HP: 28 </em>

<em>Boromir wins! </em>

<h2>False</h2>

&gt;&gt;&gt; duel(orc3,sean_bean)

<em>Orc – HP: 12 </em>

<em>Boromir – HP: 28 </em>

<em>Orc attacks Boromir for 16 damage </em>

<em>Boromir attacks Orc for 16 damage </em>

<em>Orc – HP: -4 </em>

<em>Boromir – HP: 12 </em>

<em>Boromir wins! </em>

<h2>False</h2>

&gt;&gt;&gt; duel(orc4,sean_bean)

<em>Orc – HP: 12 </em>

<em>Boromir – HP: 12 </em>

<em>Orc attacks Boromir for 16 damage </em>

<em>Orc – HP: 12 </em>

<em>Boromir – HP: -4 </em>

<em>Orc wins! </em>

<h2>True</h2>

&gt;&gt;&gt; duel(sean_bean,orc1)

<em>Boromir – HP: -4 </em>

<em>Orc – HP: -4 </em>

<em>Everyone loses! </em>

<strong>False </strong>

<strong> </strong>

<strong> </strong>




<h1>Problem B. (10<em> points</em>) <strong>The Ultimate Showdown</strong></h1>

You have decided to implement a tournament feature within your RPG.  Since you want the winner to be somewhat unpredictable, you come up with a scheme to keep the playing field as balanced as possible despite widely varying ability levels: for each round, the two Adventurers with the highest remaining HP will be forced to fight each other until one of them is eliminated.  This will hopefully keep the weaker characters in the tournament until the stronger characters have worn each other down.




Create a function called tournament(adv_list), which takes in a single parameter, a list of Adventurer objects adv_list, and pits them against each other until there is a single winner to return.  Specifically:

<ul>

 <li>If adv_list is empty, tournament should return None.</li>

 <li>If adv_list contains exactly one Adventurer object, tournament should return that Adventurer</li>

 <li>Otherwise, tournament should do the following until there is only one Adventurer object remaining:</li>

</ul>

○ Sort adv_list by current HP.  You may want to create a key function that returns the current HP of a given Adventurer object to use with the built-in sorted(), or overload the &lt; operator for Adventurer, similar to Homework 10.

○ Pass the second highest HP Adventurer and the highest HP Adventurer into the duel function (in that order, so that the second highest HP Adventurer gets to strike first).  You may assume that no Adventurer object is in the tournament list multiple times or entered the tournament list while already at 0 or less HP, so duel is guaranteed to have a clear winner.

○ Whichever Adventurer lost the duel is removed from adv_list, and the process repeats.  Remember to re-sort the list, as the winner of the duel may now have substantially less HP.




<strong>Constraints</strong>:

<ul>

 <li>Your file should only contain class definitions and functions. No code should be included outside of the classes/functions (though, as usual, comments are fine).</li>

 <li>You must name all classes, methods, and instance variables EXACTLY as specified.</li>

 <li>You should not import any modules.</li>

</ul>




<strong>Examples:</strong> (<em>italic text</em> is printed, <strong>bold text</strong>is returned)




Example 1:




&gt;&gt;&gt; print(tournament([]))

None

Example 2:




&gt;&gt;&gt; mario = Wizard(“Mario”,8,4,4,2)

&gt;&gt;&gt; link = Fighter(“Link”,7,4,2,1)

&gt;&gt;&gt; fox = Thief(“Fox”,9,2,4,2)

&gt;&gt;&gt; ness = Wizard(“Ness”,6,1,1,4)

&gt;&gt;&gt; smashls = [mario,link,fox,ness]

&gt;&gt;&gt; winner = tournament(smashls)

<em>Fox – HP: 72 </em>

<em>Link – HP: 84 </em>

<em>Fox sneak attacks Link for 65 damage </em>

<em>Link attacks Fox for 14 damage </em>

<em>Fox – HP: 58 </em>

<em>Link – HP: 19 </em>

<em>Fox attacks Link for 6 damage </em>

<em>Link attacks Fox for 14 damage </em>

<em>Fox – HP: 44 </em>

<em>Link – HP: 13 </em>

<em>Fox attacks Link for 6 damage </em>

<em>Link attacks Fox for 14 damage </em>

<em>Fox – HP: 30 </em>

<em>Link – HP: 7 </em>

<em>Fox attacks Link for 6 damage </em>

<em>Link attacks Fox for 14 damage </em>

<em>Fox – HP: 16 </em>

<em>Link – HP: 1 </em>

<em>Fox attacks Link for 6 damage </em>

<em>Fox – HP: 16 </em>

<em>Link – HP: -5 </em>

<em>Fox wins! </em>

<em>Ness – HP: 36 </em>

<em>Mario – HP: 48 </em>

<em>Ness casts fireball on Mario for 18 damage </em>

<em>Mario casts fireball on Ness for 24 damage </em>

<em>Ness – HP: 12 </em>

<em>Mario – HP: 30 </em>

<em>Ness casts fireball on Mario for 18 damage </em>

<em>Mario casts fireball on Ness for 24 damage </em>

<em>Ness – HP: -12 </em>

<em>Mario – HP: 12 </em>

<em>Mario wins! </em>

<em>Mario – HP: 12 </em>

<em>Fox – HP: 16 </em>

<em>Mario attacks Fox for 8 damage </em>

<em>Fox attacks Mario for 6 damage </em>

<em>Mario – HP: 6 </em>

<em>Fox – HP: 8 </em>

<em>Mario attacks Fox for 8 damage </em>

<em>Mario – HP: 6 </em>

<em>Fox – HP: 0 Mario wins! </em>

&gt;&gt;&gt; winner.name

<h2>‘Mario’</h2>




Example 3:




&gt;&gt;&gt; jaina = Wizard(“Jaina”,15,1,2,6)

&gt;&gt;&gt; frisk = Fighter(“Frisk”,1,1,1,1)

&gt;&gt;&gt; madeline = Thief(“Madeline”,4,1,10,1)

&gt;&gt;&gt; gandalf = Wizard(“Gandalf”,19,4,3,1)

&gt;&gt;&gt; arthur = Fighter(“Arthur”,3,4,4,4)

&gt;&gt;&gt; wesley = Thief(“Wesley”,14,4,5,1)

&gt;&gt;&gt; winner = tournament([jaina,frisk,madeline,gandalf,arthur,wesley])

<em>Wesley – HP: 112 </em>

<em>Gandalf – HP: 114 </em>

<em>Wesley sneak attacks Gandalf for 95 damage </em>

<em>Gandalf casts fireball on Wesley for 57 damage </em>

<em>Wesley – HP: 55 </em>

<em>Gandalf – HP: 19 </em>

<em>Wesley attacks Gandalf for 8 damage </em>

<em>Gandalf attacks Wesley for 8 damage </em>

<em>Wesley – HP: 47 </em>

<em>Gandalf – HP: 11 </em>

<em>Wesley attacks Gandalf for 8 damage </em>

<em>Gandalf attacks Wesley for 8 damage </em>

<em>Wesley – HP: 39 </em>

<em>Gandalf – HP: 3 </em>

<em>Wesley attacks Gandalf for 8 damage </em>

<em>Wesley – HP: 39 Gandalf – HP: -5 </em>

<em>Wesley wins! </em>

<em>Wesley – HP: 39 </em>

<em>Jaina – HP: 90 </em>

<em>Wesley attacks Jaina for 8 damage </em>

<em>Jaina casts fireball on Wesley for 45 damage </em>

<em>Wesley – HP: -6 Jaina – HP: 82 </em>

<em>Jaina wins! </em>

<em>Arthur – HP: 36 </em>

<em>Jaina – HP: 82 </em>

<em>Arthur attacks Jaina for 14 damage </em>

<em>Jaina casts fireball on Arthur for 45 damage </em>

<em>Arthur – HP: -9 Jaina – HP: 68 </em>

<em>Jaina wins! </em>

<em>Madeline – HP: 32 </em>

<em>Jaina – HP: 68 </em>

<em>Madeline sneak attacks Jaina for 70 damage </em>

<em>Madeline – HP: 32 </em>

<em>Jaina – HP: -2 Madeline wins! </em>

<em>Frisk – HP: 12 </em>

<em>Madeline – HP: 32 </em>

<em>Frisk attacks Madeline for 8 damage </em>

<em>Madeline attacks Frisk for 5 damage </em>

<em>Frisk – HP: 7 </em>

<em>Madeline – HP: 24 </em>

<em>Frisk attacks Madeline for 8 damage </em>

<em>Madeline attacks Frisk for 5 damage </em>

<em>Frisk – HP: 2 </em>

<em>Madeline – HP: 16 </em>

<em>Frisk attacks Madeline for 8 damage </em>

<em>Madeline attacks Frisk for 5 damage </em>

<em>Frisk – HP: -3 </em>

<em>Madeline – HP: 8 </em>

<em>Madeline wins! </em>

&gt;&gt;&gt; winner.name

<h2>‘Madeline’</h2>


