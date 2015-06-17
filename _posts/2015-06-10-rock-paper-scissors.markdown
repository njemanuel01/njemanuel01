---
layout: post
title:  "Rock Paper Scissors"
date:   2015-06-10
categories: code
---

# Rock Paper Scissors Lizard Spock
I built a program to execute a game of "Rock, Paper, Scissors, Lizard, Spock."  The game can be played against the computer or against another user.  I use the GamerDriver class to run the game, the Matches class to run each match of the game, the Player class to create instances of human players, and the ComputerPlayer class to create an instance of a computer player if one is required.

##app.rb
This file determines if the user wants to play a game of "Rock, Paper, Scissors, Lizard, Spock" and checks the user's input to make sure it is valid.  If the user wants to start a game, it calls the GameDriver class to start a new game, if not, the program ends.

##gamedriver.rb
When game driver is called, it runs three main methods.
-player_setup
-matches
-output_result

*player_setup*
When player setup is called, it creates players based on the user input for the number of players.  If there is only one player,  the user adds a name for player1 and an instance of the Player class is called, a computer player is assigned to player2 and an instance of the ComputerPlayer class is called. If there are two players, they alternate adding names for player1 and player2, these names are used when the Player class is called for each.

```ruby
def player_setup
  player_number_entry()

  if @player_count == 1
    puts "What is your name?"
    name1 = gets.chomp
      
    @player1 = Player.new(name1)
    @player2 = ComputerPlayer.new()
  else
    puts "What is player 1's name?"
    name1 = gets.chomp
    puts "What is player 2's name?"
    name2 = gets.chomp
      
    @player1 = Player.new(name1)
    @player2 = Player.new(name2)
  end
end
```

*matches*
After the players are setup, the matches method is called.  This method asks the user for the number of matches to run for the game and then runs each instance of those matches.

```ruby
def matches
  self.get_match_count
  self.run_matches
end
```

The run_matches method gets each players' move for each of the matches.  The method runs until either one of the players has won enough matches to meet the win condition or until all matches have been run.  It also adds a point to the total score of a player when they win a match and outputs the result of each match to the screen.

```ruby
def run_matches
  self.win_condition
  while @match_count > 0
    self.get_valid_entries()

    puts @game.match_result
      
    @match_count -= 1
    if ((@player1.score == @win_condition) || (@player2.score == @win_condition))
      break
    end
  end
end
```
*output_result*
Lastly, the output result method prints the game results to the screen as well as a text file whose name is tied to the token for each instance of a game being run.

```ruby
def output_result
  puts "The final score was: #{@player1.name} = #{@player1.score}, #{@player2.name} = #{@player2.score}"
  puts @game.game_result
    
  file1 = File.open(@game.to_s, 'w')
  file1.puts @game.game_result
  file1.close
end 
```
##match.rb
When the Matches class is called, it tests each user's move to see which one has won the match.  It returns a string for the GameDriver to output to the screen and adds one point to the match winner's score.  It also calculates the game winner based on the scores of each player.  It returns that result to the GameDriver as a string and also outputs the result to a text file.

Here is the code to determine the winner of each match:

```ruby
def match_result
  if (((@player1.move == 'Rock' && @player2.move == 'Scissors') || (@player1.move == 'Rock' && @player2.move == 'Lizard')) || 
  ((@player1.move == 'Paper' && @player2.move == 'Rock') || (@player1.move == 'Paper' && @player2.move == 'Spock')) || 
  ((@player1.move == 'Scissors' && @player2.move == 'Paper') || (@player1.move == 'Scissors' && @player2.move == 'Lizard')) ||
  ((@player1.move == 'Lizard' && @player2.move == 'Paper') || (@player1.move == 'Lizard' && @player2.move == 'Spock')) ||
  ((@player1.move == 'Spock' && @player2.move == 'Scissors') || (@player1.move == 'Spock' && @player2.move == 'Rock')))
      
    @player1.add_score
    return "#{@player1.move} beats #{@player2.move}: #{@player1.name} wins the match!!!"
  elsif (((@player2.move == 'Rock' && @player1.move == 'Scissors') || (@player2.move == 'Rock' && @player1.move == 'Lizard')) || 
  ((@player2.move == 'Paper' && @player1.move == 'Rock') || (@player2.move == 'Paper' && @player1.move == 'Spock')) || 
  ((@player2.move == 'Scissors' && @player1.move == 'Paper') || (@player2.move == 'Scissors' && @player1.move == 'Lizard')) ||
  ((@player2.move == 'Lizard' && @player1.move == 'Paper') || (@player2.move == 'Lizard' && @player1.move == 'Spock')) ||
  ((@player2.move == 'Spock' && @player1.move == 'Scissors') || (@player2.move == 'Spock' && @player1.move == 'Rock'))) 
    
  @player2.add_score
    return "#{@player2.move} beats #{@player1.move}: #{@player2.name} wins the match!!!"
  else
    return 'The match was a tie'
  end
end
```

##player.rb
The Player class creates a new object for human players and stores the player's name, move for a match, and total score for a game.

```ruby
def initialize(name)
  @name = name
  @move = ""
  @score = 0
end
```

##computer.rb
The ComputerPlayer class creates a new object of a computer player that randomly selects a "move" from an array.  It also stores a name, move for a match, and a total score for a game.

```ruby
def initialize()
  @name = 'Computer'
  @move = ""
  @score = 0
end
```

```ruby
def get_move
  @move = ['Rock', 'Paper', 'Scissors', 'Lizard', 'Spock'].sample
  puts @move
end
```
