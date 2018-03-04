
# class Game                                             
## public
### \_\_init\_\_
__inputs:__    none  
__returns:__    none  
__description__  
sets currentPlayer to 1  
sets gameState to initial GameState (blank board)  
sets actionSpace to blank array the size of the board  
sets pieces to dict {'1':'X', '0': '-', '-1':'O'}  
sets grid_shape to board size 6x7  
sets input_shape to 2xboard size  
sets name  
sets state_size to length of gameState.binary  
sets action_size to length of actionSpace  

### reset
__inputs:__    none  
__returns:__    GameState  
__description__  
returns initial GameState ie blank board
also sets currentPlayer to 1

### step
__inputs:__ action  
__returns:__ (next_state, value, done, None)  
__description__  
returns the next state based on the current state and action takeAction  
also sets currentPlayer to -currentPlayer ? to indicate whose turn it is

### identities
__inputs:__ state, actionValues  
__returns:__ [(state,actionValues),(GameState(currentBoard, state.playerTurn), currentAV)]  
__description__  
? returns the input and its mirror

# class GameState
## public
#### \_\_init\_\_
__inputs:__ board, playerTurn  
__returns:__ new GameState  
sets board to input board  
sets pieces to {'1':'X', '0': '-', '-1':'O'}  
sets winners to list of 4 in a row tiles  
sets playerTurn to input playerTurn  
sets binary to _binary()  
sets id to _convertStateToId()  
sets allowedActions to _allowedActions()  
sets isEndGame to _checkForEndGame()  
sets value to _getValue()  
sets score to _getScore()  

### takeAction
__inputs:__ action  
__returns:__ (newState,value,done)  
creates a new board then applies playerTurn to the currentBoard  
from this creates a new GameState  
done = 1 if endgame reached, 0 otherwise  
value = -1 if other player won, 0 otherwise  

### render
__inputs:__ logger  
__returns:__ None  
__description__  
prints the board with logger

## private

### \_allowedActions
__inputs:__ None  
__returns:__ list of allowed indices where an action can be taken  
e.g. for connect4 returns the spots where a placed piece would fall to  

### \_binary
__inputs:__ None  
__returns:__ position
__description__  
position is a numpy array that looks like [currentplayer_position, other_position]  
where currentplayer_position is 1 for all the spots on the board the player is, 0 otherwise  
and other_position is 1 for all the spots on the board the other player is, 0 otherwise  

### \_convertStateToId
__inputs:__ none  
__returns:__ id (string)  
a unique id for the current game state. e.g. a ''.join(map(str, _binary()))

### \_checkForEndGame
__inputs:__ None  
__returns:__ 1 if board is full or other player has won, 0 otherwise

### \_getValue
__inputs:__ None  
__returns:__ (-1,-1,1) if other player has won, (0,0,0) otherwise

### \_getScore
__inputs:__ None  
__returns:__ (self.value[1], self.value[2])  
__description__  
does not call _getValue  
? returns (-1,1) if other player has won, (0,0) otherwise
