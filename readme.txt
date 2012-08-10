Title: XHR Tower Defence
Author: Benjamin Meier MRXBEN001
Date: August 2012
Github Repo: https://github.com/AstromechZA/Tower_Defence

-----------------------------------------
CONTENTS
----------------
[1]: Introduction
[2]: Tower Types
[3]: Enemy Types
[4]: Technical
[5]: Cheats for testing
----------------

[1: Introduction]
This game is a simple tower defence game made for my CSC2003S Game development course at UCT. It is a 
tower defence in that the enemies (The Unknowns) move towards the goal (The laboratory) and must be 
stopped by building towers along their path. In this game, the enemies do not follow a fixed path but 
use a reverse breadth-first search to reach the goal. Thus their path can be manipulated and lengthened 
by building towers in their way.

[2: Tower Types]
[2.1: Gun Tower]
	A simple rapid fire tower, useful in early to mid game. Its upgrades double and then triple its rate of fire.
	
	Initial:
		Cost: 			100
		Damage: 		5
		Rate of Fire: 	6
	Upgrade 1:
		Cost:			100
		Damage:			5
		Rate of Fire:	12
	Upgrade 2:
		Cost:			100
		Damage:			5
		Rate of Fire:	18

[2.2: Cannon Tower]
	A slower firing tower that does significant damage. Its upgrades multiply its damage.
	
	Initial:
		Cost: 			300
		Damage: 		25
		Rate of Fire: 	1.5
	Upgrade 1:
		Cost:			200
		Damage:			42
		Rate of Fire:	1.5
	Upgrade 2:
		Cost:			200
		Damage:			63
		Rate of Fire:	1.5

[2.3: Rocket Tower]
	Rocket towers are capable of engaging enemies from long range. It fires a guided projectile that 
	locks onto a single target. if that target is destroyed it explodes at the targets last known position. 
	Upgrading a rocket tower improves its rate of fire.
	
	Initial:
		Cost: 			300
		Damage: 		40
		Rate of Fire: 	0.5
	Upgrade 1:
		Cost:			200
		Damage:			80
		Rate of Fire:	0.5
	Upgrade 2:
		Cost:			200
		Damage:			120
		Rate of Fire:	0.5
	
[2.4: Sonic Tower]
	The sonic tower releases a wave on energy that slows down any enemies around the tower. 
	Upgrades improve its firing rate.
	
	Initial:
		Cost: 			300
		Damage: 		-
		Rate of Fire: 	0.3
	Upgrade 1:
		Cost:			200
		Damage:			-
		Rate of Fire:	0.4
	Upgrade 2:
		Cost:			200
		Damage:			-
		Rate of Fire:	0.6

[2.5: Lightning Tower]
	The lightning tower is an expensive late-game tower that releases a beam of lightning 
	that jumps between up to 4 nearby enemies. It does damage over time that can be improved 
	by upgrading the tower.
	
	Initial:
		Cost: 			1000
		Damage: 		3,3,2,1
		Rate of Fire: 	30
	Upgrade 1:
		Cost:			2000
		Damage:			6,6,4,2
		Rate of Fire:	30
	Upgrade 2:
		Cost:			2500
		Damage:			9,9,6,3
		Rate of Fire:	30

[3: Enemy Types]
	There are 8 different varieties of Unknowns in this game:
	# Small				-	Small and fast, low health
	# Small (Shielded)
	# Medium			-	Standard enemy.
	# Medium (Shielded)	
	# Big				-	Larget and slow but with a lot of health
	# Big (Shielded)	
	# Uber				-	Large, Fast, lots of health.
	# Uber (Shielded)

	The shielded versions of enemies have a blue energy shield around them that effectively doubles their health.

[4: Technical]
[4.1: Artifical Intelligence]
	When the room is initialised the pathController object creates an 2D array of cells that matches 
	the number of 32x32 grid cells in the room. There is a script called gen_AI() which populates 
	this array with 0,1,2,3 for right, up, left, down; -1 to indicate the cell is blocked or 1337 
	to indicate it is unreachable. The direction values are used by enemies to find the next grid 
	cell they need to go to. Once the enemy comes within 3 pixels of its waypoint it finds its next 
	waypoint by consulting the 2D array of directions. The 2D array of directions is populated by 
	performing a breadth first fill from the goal (the laboratory) outwards. This fills the unblocked 
	cells with directions that effectively allow any enemy to find the shortest path from its current 
	position to the goal. Because gen_AI() is called whenever a tower is built, enemies can find their 
	way towards the goal irrespective of their previous paths or directions. 
	To view the AI overlay in game, hold down the P key. 
	
[4.2: Tower AI]
	Gun towers and cannon towers need to be pointing at their targets in order to fire. This means that 
	every step the tower finds its current target, rotates towards it if needed, and then attempts to fire.
	
	Lightning Towers are relatively complex as at each step they attempt to string together up to 4 enemies. 
	Note that these 4 enemies are not simply the 4 enemies closest to the tower, but are the closest string of enemies:
	Enemy 1 = closest to tower
	Enemy 2 = closest to enemy 1
	Enemy 3 = closest to enemy 2
	Enemy 4 = closest to enemy 3
	The script also makes sure that it does not hit the same enemy multiple times in 1 beam.
	
[5: Cheats for testing]

	P (hold): 	show AI overlay
	
	O:			add $50
	
	I:			restore laboratory health
	
-------------------------------------------------------------------