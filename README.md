# first-game-
from IPython.display import clear_output

def display_board(board):
    clear_output()
    print('---------------')
    print('|   |    |   |')
    print('| ' +   board[7] + ' | ' + board[8] + '  | ' + board[9] + ' | ')
    print('|   |    |   |')
    print('---------------')
    print('|   |    |   |')
    print('| ' +   board[4] + ' | ' + board[5] + '  | ' + board[6] + ' | ')
    print('|   |    |   |')
    print('---------------')
    print('|   |    |   |')
    print('| ' +   board[1] + ' | ' + board[2] + '  | ' + board[3] + ' | ')
    print('|   |    |   |')
    print('---------------')
In [2]:
def player_input():
    gamecoin=''
    while not (gamecoin=='x' or gamecoin=='o'):
        print "do u want x or o mr.player1:"
        gamecoin=raw_input()
    if gamecoin=='x':
        return ('x','o')
    else:
        return ('o','x')
In [3]:
def place_marker(board, marker, position):
    board[position] = marker
In [4]:
def win_check(board,mark):
    
    return ((board[7] == mark and board[8] == mark and board[9] == mark) or # across the top
    (board[4] == mark and board[5] == mark and board[6] == mark) or # across the middle
    (board[1] == mark and board[2] == mark and board[3] == mark) or # across the bottom
    (board[7] == mark and board[4] == mark and board[1] == mark) or # down the middle
    (board[8] == mark and board[5] == mark and board[2] == mark) or # down the middle
    (board[9] == mark and board[6] == mark and board[3] == mark) or # down the right side
    (board[7] == mark and board[5] == mark and board[3] == mark) or # diagonal
    (board[9] == mark and board[5] == mark and board[1] == mark)) # diagonal
In [5]:
def space_check(board, position):
    
    return board[position] == ' '
In [6]:
def full_board_check(board):
    for i in range(1,10):
        if space_check(board, i):
            return False
    return True
In [7]:
import random
def choose_first():
    if random.randint(0, 1) == 0:
        return 'Player 2'
    else:
        return 'Player 1'
In [8]:
def player_choice(board):
    # Using strings because of raw_input
    position = ' '
    while position not in '1 2 3 4 5 6 7 8 9'.split() or not space_check(board, int(position)):
        
        position = raw_input('Choose your next position: (1-9) ')
    return int(position)
In [9]:
def replay():
    
    return raw_input('Do you want to play again? Enter Yes or No: ').lower().startswith('y')
In [10]:
print('Welcome to Tic Tac Toe!')

while True:
    # Reset the board
    theBoard = [' '] * 10
    player1_marker, player2_marker = player_input()
    turn = choose_first()
    print(turn + ' will go first.')
    game_on = True

    while game_on:
        if turn == 'Player 1':
            # Player1's turn.
            
            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player1_marker, position)

            if win_check(theBoard, player1_marker):
                display_board(theBoard)
                print('Congratulations! You have won the game!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('The game is a draw!')
                    break
                else:
                    turn = 'Player 2'

        else:
            # Player2's turn.
            
            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player2_marker, position)

            if win_check(theBoard, player2_marker):
                display_board(theBoard)
                print('Player 2 has won!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('The game is a tie!')
                    break
                else:
                    turn = 'Player 1'

    if not replay(
        break
---------------
|   |    |   |
| o | o  | x | 
|   |    |   |
---------------
|   |    |   |
| x | o  | x | 
|   |    |   |
---------------
|   |    |   |
| o | x  | x | 
|   |    |   |
---------------
Player 2 has won!
Do you want to play again? Enter Yes or No: n

 
