# python-tic-tac-toe-project
#Araceli

'''
This function displays a working tic-tac-toe board.
When a player chooses a location on the board, their
choice will be placed in a list according to the
index. Choices are from zero to eight.
'''

def display_board(board):
    print(board[0]+'|'+board[1]+'|'+board[2])
    print('-|-|-')
    print(board[3]+'|'+board[4]+'|'+board[5])
    print('-|-|-')
    print(board[6]+'|'+board[7]+'|'+board[8])
    print()
#Test:
#test_board_1 = ["x","o","x","o","x","o","x","o","x"]
#display_board(test_board_1)
    
        
'''
This function ask which sign, "x" or "o", the player wants.
If the player chooses anything other than 'x or o' the
function will keep asking.
'''

def player_input():
    
    sign = ''
    
    while sign != 'x' and sign != 'o':
        
        sign = input('Player 1, choose x or o: ').lower()
    
        player1 = sign
    
    
        if player1 == 'x':
            player2 = 'o'
        else:
            player2 = 'x'
    return(player1,player2)
#Test:
#Note, try other signs instead of 'x or o'.
#player_input()


'''
This function will show the current status of the
board when the user chooses a location.
'''

def enter_move(board, sign, location):
    board[location] = sign
#Test:
#Note, need fucntion display_board().
#test_board_1 = ["x","o","x","o","x","o","x","o","x"]
#test_sign = "R"
#test_location = 1
#enter_move(test_board_1,test_sign,test_location)
#display_board(test_board_1)


'''
This function checks all eight possiblities of
winning at Tic Tac Toe:
Three rows, three columns or two diagonals.
During testing you need to use print() to determine
if the boolean is True or False.
'''

def victory_for(board, sign):
    return ((board[0] == sign and board[1] == sign and board[2] == sign) or #Top Row
            (board[3] == sign and board[4] == sign and board[5] == sign ) or #Middle Row
            (board[6] == sign and board[7] == sign and board[8] == sign ) or #Bottom Row
            (board[0] == sign and board[3] == sign and board[6] == sign ) or #1st Column
            (board[1] == sign and board[4] == sign and board[7] == sign ) or #2nd Column
            (board[2] == sign and board[5] == sign and board[8] == sign ) or #3rd Column
            (board[0] == sign and board[4] == sign and board[8] == sign ) or #Left Diagonal
            (board[2] == sign and board[4] == sign and board[6] == sign )) #Right Diagonal
#Test:
#Note, need fucntion display_board().
#test_board_1 = ["x","o","x","o","x","o","x","o","o"]
#test_sign_1 = "x"
#test_sign_2 = "o"
#display_board(test_board_1)
#print(victory_for(test_board_1, test_sign_1))
#print(victory_for(test_board_1, test_sign_2))


'''
This function uses the randint() method from the
randdom module to choose which player goes first.
This is like flipping a coin.
'''

import random
def who_goes_first():
    flip = random.randint(0,1)
    if flip == 0:
        print("Player 1 goes first.")
        return "Player 1"
    else:
        print("Player 2 goes first.")
        return "Player 2"
#Test:
#who_goes_first()


'''
This function checks to see if a chosen location on
the board is empty.  It will be used inside another
function that will check if the board is full and
another function that checks the players choice
of location on the board. 
'''

def location_check(board, location):
    return board[location] == ' '
#Test:
#test_board_1 = ["x","o","x","o","x","o","x","o","o"]
#test_board_2 = ["x","o","x","o"," ","o","x","o","o"]
#print(location_check(test_board_1, 4))
#print(location_check(test_board_2, 4))


'''
This function checks to see if there are no more available
locations left on the board.  It will use the space_check()
function.
'''

def full_board_check(board):
    for i in range(0,9):
        if location_check(board,i):
            return False
    return True
#Test:
#Note, need fucntion location_check().
#test_board_1 = ["x","o","x","o","x","o","x","o","o"]
#test_board_2 = ["x","o","x","o"," ","o","x","o","o"]
#print(full_board_check(test_board_1))
#print(full_board_check(test_board_2))


'''
This function checks to see if it's an actual location on the
board or if the location is available.
'''

def player_choice(board):
    location = 9 #Just make it a location that doesn't exist on the board.
    
    while location not in [0,1,2,3,4,5,6,7,8] or not location_check(board,location):
        location = int(input('Choose a location from 0 to 8: '))
        return location
#Test:
#Note, need fucntion location_check().
#test_board_1 = ["x","o","x","o","x","o","x","o","o"]
#test_board_2 = ["x","o","x","o"," ","o","x","o","o"]
#player_choice(test_board_1)
#print(player_choice(test_board_1))
#print()
#player_choice(test_board_2)
#print(player_choice(test_board_2))


 

def replay():
    play_again = input('Would you like to play again? y or n: ')
    
    if play_again.lower() == 'y':
        return True
    
    else:
        return False
#Test:
#Note, test both 'y' and 'n'.
#print(replay())
    

'''
This runs the game.  The TEST is if it works.
'''

print("="*40)    
print('Welcome to Tic Tac Toe!')
print("Number indicates location on the board.")
print()
print("0"+'|'+"1"+'|'+"2")
print('-|-|-')
print("3"+'|'+"4"+'|'+"5")
print('-|-|-')
print("6"+'|'+"7"+'|'+"8")
print("="*40)
print()

#WHILE loop to keep running the game.
while True:
    
    #Set everything up (board, who's first, choose signs 'x or o')
    the_board = [' ']*9
    player1_sign,player2_sign = player_input()
    
    #The coin flip function.
    first = who_goes_first()
    
    #Report who goes first.
    print(first + ' will go first!')

    #Ask if ready to play the game.
    game_ready = input('Are you ready to play? y or n? ')
    if game_ready == 'y':
        game_on = True
    else:
        game_on = False
        
    #Play the game.
    while game_on:
        #Player 1's move.
        if first == 'Player 1':
            
            #Show board.
            display_board(the_board)
            
            #Choose location.
            location = player_choice(the_board)

            #Place the sign on the location.
            enter_move(the_board,player1_sign,location)
            
            #Check to see if Player 1 won.        
            if victory_for(the_board,player1_sign):
                display_board(the_board)
                print('Player 1 has won!')

                #This will break out of 'while game_on' loop
                #if Player 1 has won.
                game_on = False

            #If Player 1 has not won then check to see if
            #it's a tie or if it's Player 2's move.
            else:

                #If board is full then it's a tie
                if full_board_check(the_board):
                    display_board(the_board)
                    print('The game is a tie!')

                    #This will break out of 'while game_on' loop
                    #if it's a tie.
                    game_on = False

                #Otherwise, it's Player 2's move.    
                else:
                    first = 'Player 2'

        #Player 2's move.  Note, same comments as Player 1's move.            
        else:
            display_board(the_board)
            location = player_choice(the_board)
            enter_move(the_board,player2_sign,location)
            
            if victory_for(the_board,player2_sign):
                display_board(the_board)
                print('Player 2 has won!')
                game_on = False
            else:
                if full_board_check(the_board):
                    display_board(the_board)
                    print('The game is a tie!')
                    game_on = False
                else:
                    first = 'Player 1'   
        
    if not replay():
        break
