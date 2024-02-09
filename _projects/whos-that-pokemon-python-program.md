---
layout: project
title: "Who's That Pokemon Python Program"
caption: A Hangman inspired Who's That Pokemon game!
description: >
  A Hangman inspired Who's That Pokemon game!
date: '2024-02-09'
image: 
  path: /assets/img/projects/whosthatpokemon/cover.jpg
accent_image: 
  background: url('/assets/img/projects/whosthatpokemon/cover.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
invert_sidebar: true
sitemap: false
---

# Who's That Pokemon?!

This is a simple python program that allows you to play a hangman inspired version of "Who's That Pokemon?!"

The game is run from the command line.  You'll want to make sure you <code>pip install pokemon</code> prior to playing.  

Pretty fun to put together :)

<img src="/assets/img/projects/whosthatpokemon/game.png">

```python

# "Who's that Pokemon?!" Python Game
# Make sure to pip install pokemon before playing!
import pokemon
from random import choice
from pokemon.master import catch_em_all, get_pokemon
from pokemon.skills import get_ascii
from collections import Counter

# catch_em_all returns the entire database of pokemon.  choices is a list of pokemon keys.
pokemons = catch_em_all()
choices = list(pokemons.keys())

# randomly pulls a secret pid. Use strpid to pull relevant info from pokemons dictionary.
pid = int(choice(choices))
strpid = str(pid)
mon = pokemons[strpid]

# pokemons dictionary contains some extra information.  we just want the name!
name = mon.get("name")
name = name.lower()


if __name__ == '__main__':
	print()
	print("A Hangman Inspired 'Who's That Pokemon' Game!")
	print()
	print("HINT: names are all in lowercase.  Start by guessing a letter!")
	print()
	print()
	
	# pull a random pokemon ascii image
	get_ascii(pid=pid, message="Who's that Pokemon?!")
	
	# Creates empty spaces for each letter in pokemon name
	for i in name:
		print('_', end=' ')
	print()
	
	playing = True
	# used to store letter guesses
	letterGuessed = ''
	chances = len(name) + 2
	correct = 0
	flag = 0
	try:
		while (chances != 0) and flag == 0: # flag updates when pokemon is guessed correctly
			print()
			chances -= 1
			
			try:
				guess = str(input('Enter a letter to guess: '))
			except:
				print('Enter only a letter!')
				continue
			
			# Guess validation
			if not guess.isalpha():
				print('Enter only a LETTER')
				continue
			elif len(guess) > 1:
				print('Enter only a SINGLE letter')
				continue
			elif guess in letterGuessed:
				print('You have already guessed that letter')
				continue
				
			# If guess is correct
			if guess in name:
				k = name.count(guess)
				for _ in range(k):
					letterGuessed += guess
			
			# Print the pokemon name
			for char in name:
				if char in letterGuessed and (Counter(letterGuessed) != Counter(name)):
					print(char, end=' ')
					correct += 1
				elif (Counter(letterGuessed) == Counter(name)):
					print("It's ", end=' ')
					print(name, "!")
					flag = 1
					print('You guessed that Pokemon!!')
					break
					break
				else:
					print('_', end=' ')
				
		# If chances are all used up
		if chances >= 0 and (Counter(letterGuessed) != Counter(name)):
			print()
			print()
			print('You lost!')
			print()
			print("It's {}".format(name))
	
	except KeyboardInterrupt:
		print()
		print('Do you want to be the very best...?')
		print()
		print('Like noone ever was...?')
		print()
		print('Try again!')
		exit()
	
```
