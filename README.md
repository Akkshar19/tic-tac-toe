# tic-tac-toe
from IPython.display import clear_output

def display_board(board):
    
    
    print(board[7] + " | " + board[8] + " | "+ board[9])
    print("----------")
    print(board[4] + " | " + board[5] + " | " + board[6])
    print("----------")
    print(board[1] + " | " + board[2] + " | " + board[3])

def player_input():
    marker=''
    while not (marker == 'X' or marker == 'O'):
        marker = input('Player 1: Do you want to be X or O? ').upper()
    if marker=='X':
        return ('X', 'O')
    else:
        return ('O', 'X')
player1_marker,player2_marker=player_input()
def place_marker(board,marker,position):
    board[position]=marker

def win_check(board,mark):
    return ((board[7] == mark and board[8] == mark and board[9] == mark) or 
    (board[4] == mark and board[5] == mark and board[6] == mark) or 
    (board[1] == mark and board[2] == mark and board[3] == mark) or 
    (board[7] == mark and board[4] == mark and board[1] == mark) or 
    (board[8] == mark and board[5] == mark and board[2] == mark) or 
    (board[9] == mark and board[6] == mark and board[3] == mark) or 
    (board[7] == mark and board[5] == mark and board[3] == mark) or 
    (board[9] == mark and board[5] == mark and board[1] == mark)) 

import random
def choose_first():
    if random.randint(0,1)==0:
        return  'Player2'
    else:
        return "Player 1"
def space_check(board, position):
    
    return board[position] == ' '

def full(board):
    for i in range(1,10):
        if space_check(board,i):
            return False
    
    return True


def player_choice(board):
    position=0
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board,position):
        position=int(input('choose your position (0-9)?'))
        if position not in [1,2,3,4,5,6,7,8,9]:
            print("Plz enter a valid position:")
    return position

def replay():
    return input("do you play again Yes or no")

print('Welcome to Tic Tac Toe!')

while True:
    # Reset the board
    board = [' '] * 10
    player1_marker, player2_marker = player_input()
    turn = choose_first()
    print(turn + ' will go first.')
    
    play_game = input('Are you ready to play? Enter Yes or No.')
    
    if play_game.lower()[0] == 'y':
        game_on = True
    else:
        game_on = False

    while game_on:
        if turn == 'Player 1':
            # Player1's turn.
            
            display_board(board)
            position = player_choice(board)
            place_marker(board, player1_marker, position)

            if win_check(board, player1_marker):
                display_board(board)
                print('Congratulations! You have won the game!')
                game_on = False
            else:
                if full(board):
                    display_board(board)
                    print('The game is a draw!')
                    break
                else:
                    turn = 'Player 2'

        else:
            # Player2's turn.
            
            display_board(board)
            position = player_choice(board)
            place_marker(board, player2_marker, position)

            if win_check(board, player2_marker):
                display_board(board)
                print('Player 2 has won!')
                game_on = False
            else:
                if full(board):
                    display_board(board)
                    print('The game is a draw!')
                    break
                else:
                    turn = 'Player 1'

    if not replay():
        break
