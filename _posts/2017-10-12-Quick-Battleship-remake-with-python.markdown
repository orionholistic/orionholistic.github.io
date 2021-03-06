---
layout: post
title:  Quick Battleship remake with Python
date:   2017-10-12 10:50:37 +0000
categories: python
---

This is a very quick and simple remake of the classic game Battleship using a single python file. The user is given 4 chances to guess the row and column of a randomly generated position on the gameboard. Our gameboard is a 5 by 5 grid of "0"s, however you can edit this game easily and make it your own. Some examples include adding more rows/columns to make the game more challenging or use "w"s instead of "0"s to look more like waves in the ocean. Whatever you create this game is fun to play and simple to understand. 

Let's get started,

First play the game and try the destroy the battship yourself, when your finished you can find the code for the game below. 

<iframe src="https://trinket.io/embed/python/913fe8a94f?outputOnly=true&start=result" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
<br>
<br>
Now that you have an idea how the game is played lets take a look at the python code. 
<br>
<br>
This game only uses one library, the random library, so that we can create a random integer for our battleship. We are going to start by importing the randomint function from the random library. Then we create our basic game board.

{% highlight py lineos %}
# import library needed to create random numbers
from random import randint
# Create Game Board
board = []
# Creates 5 rows of ["O","O","O","O","O"]
for x in range(0, 5):
  board.append(["O"] * 5)
# removes [""] from board and leaves 5 rows of O O O O O
def print_board(board):
  for row in board:
    print " ".join(row)
# prints the Game Board
print_board(board)
{%endhighlight%}
<br>

Now its time to put the battleship on the game board. Well use the randomint function we imported earlier to get a random location each time the game is played. This way we can play as many times as we want without getting bored.
{% highlight py lineos %}
# gets random number for ship row
def random_row(board):
  return randint(0, len(board) - 1)
# gets random number for ship col
def random_col(board):
  return randint(0, len(board[0]) - 1)
{%endhighlight%}
<br>

Next assign our random location to our battleship variables. If you want to print the location of our battleship to make sure the game is working you can remove the "#"s from the print statements. 
{% highlight py lineos %}
# assigns random row and col to ship variables
ship_row = random_row(board)
ship_col = random_col(board)
# Use this to print location of ship for Debug or "Cheat"
#print ship_row
#print ship_col
{%endhighlight%}
<br>

Now that we have a battleship on our gameboard its time to create the gameplay. We gave our player 4 attempts to guess the ships location. You can adjust this easily by changing the range().
{% highlight py lineos %}
# game loop set to 4 turns
for turn in range(4):
  # show user what turn they are on
  print "Turn", turn + 1
  # Ask user for input as "guess"
  guess_row = int(raw_input("Guess Row: "))
  guess_col = int(raw_input("Guess Col: "))
{% endhighlight %}
<br>

The last thing we have to do is define what happens when the users guess is correct, incorrect, off the board, or out of turns. We do this using a serious of if/else statements. 
{% highlight py lineos %}
# if guess is correct print Congrats and Break the Game Loop
  if guess_row == ship_row and guess_col == ship_col:
    print "Congratulations! You sank my battleship!"
    break
# if guess is not correct check why
  else:
    # check to see if guess is in range "on board"
    if guess_row not in range(5) or \
      guess_col not in range(5):
      print "Oops, that's not even in the ocean."
    # check to see if user already guessed same thing
    elif board[guess_row][guess_col] == "X":
      print "You guessed that one already." 
# if guess is on board and not already guessed change board "O" to "X" and print "missed" 
    else:
      print "You missed my battleship!"
      board[guess_row][guess_col] = "X"
# End Game Loop if turn is equal to 3 or the fourth turn counted from 0
      if turn == 3:
        print "Game Over"
        # if game loop is not ended and user did not win then print game board for next turn 
    print_board(board)
{% endhighlight %}

If you enjoyed learning how to re-create this game and would like to learn more, make sure to follow this blog or check back regularly for updates. 
