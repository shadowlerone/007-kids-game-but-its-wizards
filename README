# 007 kids game but it is wizard

007 is a camp game from when I was a kid. Working at camp this year, there was a mild resurgence. One observation I have as an adult is that the game is completely unbalanced. So... I'm gonna make a video game version of it! And I'm going to completely ruin the childhood simplicity with mechanics that would never work in reality!

## Original gameplay Flow

The camp version is usually played 1v1. The flow goes something like this:

- Chant "Zero Zero Seven" while tapping your hands on your thighs
- Choose one of 3 actions:
  - Reload 	-> 	gain 1 `bullet`
  - Shoot 	->	if `bullet` > 0, consume 1 `bullet`, disabled otherwise
  - Block	-> 	protects from a shot
- See who wins.
  - If shot while reloading, you lose
  - If shot while blocking, you don't lose. The person who shot loses a `bullet`
  - If both reload, nothing happens.
  - If both shoot, no one wins. Both consume a `bullet`
- Repeat until someone loses

It is worth noting that all the game info is known to both players. Both players know each other's `bullet` count.

## Modified gameplay flow

So I don't like guns, so I'm going to reskin this game to be wizards themed. I think that for a video game adaptation, it'll be more fun and offer more options for expanding. Gotta dream big, you know. 

### Player Actions

First set of modifications: player choices. `Shoot` becomes `Firebolt`, `Block` becomes `Shield`, and `Reload` becomes `Charge` (pending). Charge gives you "mana" instead of "bullets". A new addition is `Shield charge`. One of the problems with the camp game is that there is no cost to blocking. That means the optimal strategy to not lose is to shield *all the time*. You can't *win* with this strategy but you can't lose, and it removes the fun from the game. Two options present themselves: shield charged tied to the `charge` action, *or* have a separate `charge shield` action. First prototype will have it tied to the charge action, as this will be simplest to implement. Each player would start the game with 3 (arbitrary number) `shield charges` and have a maximum of 5 (arbitrary number). It's worth noting that these values are flexible: if the game ends up having levels and progression, the max charges may be expanded, and there may be more spells with higher costs. All should be possible with the systems created, it might just be beyond the scope of this project.

Both players will still know each other's `Charge` and `Shield Charge` count, the strategy comes from predicting your opponent(s)'s next move.

### Health

In the camp game, there is no scoring system. Most of the kids don't bother counting their "points" so there's no need for a win condition beyond each individual round. The game keeps rolling until there's one person standing, and then it loops. This would be a great milestone for a first prototype, but for an actual "game" there needs to be some sense of progression. Another problem is that each `player` or `enemy` (henceforth `entity`) can only take a single hit without dying.

### Multiple targets

The camp game has a multiplayer component. You know what that means? Single target and AoE spells! 

## Goals

1. Replica of the camp game
   1. Single looped `encounter`
   2. 3 choices: `Charge`, `Block`, `Firebolt`
   3. No `Shield Charge`
   4. Command Line interface (no time for graphics)
   5. Enemy "A.I."
      1. Turn 1: `Charge`
      2. Turn 2 and onwards: if charge > 0, shuffle `Block` and `Firebolt` (50/50), else shuffle `Block` and `Charge` (50/50)
2. `Shield Charge`
   1. 3 `Shield Charge`s, max of 5
   2. Enemy "A.I." improvements (see pseudocode below)
      1. Aggressive and Defensive AI

### Enemy A.I. pseudocode

```python
# Defensive A.I.
if player.charges > 0:
	if entity.shield_charges > 0:
		return shield
	if entity.charges > 0:
		return shoot
	if entity.shield_charges < max_charges:
		return shield_charge
	return charge
elif entity.shield_charges < max_charges:
	return shield_charge
else:
	return charge

```

```python
# Aggressive A.I.
if player.last_move == "shield":
	if player.charges > 0:
		if entity.charges > 0:
			return shoot
		else:

	else:
		if entity.charges > 0
			return shoot
		else:
			return charge
```

#### Predictive A.I.

Store pairs of player actions. Based on 1st action and player data, look at probability of 2nd.

| Next Player Action / Previous A.I Action| Shoot | Block | Charge | Total |
|---------------------|--------|---------|----------|-|
| Shoot         | 11 | 12| 14| 37
| Block			| 14 | 23 | 10 | 47 |
| Charge		| 20 | 45 | 0 | 65 |
| Total			| 45 | 85 | 24 | 149

Based on a table like this, calculate the probability of events occurring.

```python
# Predictive A.I.
history = [charge, block, shoot, block, block, shoot]

```

Another one would be: look at enemy and player 1st actions and the player's 2nd action. Calculate the probability of each action and use the confidence interval to determine the weights of each action. 

| Player | Entity | Player Next Move | Probability |
|--------|--------|------------------|-------------|
| Charge | Block  | shoot			 | 			   |


```python
probabilities = {
	"charge+block": {
		"shoot": 0.1, 
		"block": 0.5, 
		"charge": 0.4
	}
}
```