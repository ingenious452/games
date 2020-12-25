# importing the required modules
import random


def get_choice(user_name):
    """Return the choice of player"""

    player_char = ''
    while not (player_char == 'X' or player_char == 'O'):
        player_char = input(f'\n{user_name} what would you like to play as(X or O): ').upper()

    if player_char == 'X':
        computer_char = 'O'
    else:
        computer_char = 'X'

    return player_char, computer_char
#-----------------------------------------

def is_winning(b, c):
    # b= board
    # c = choice(X or O)

    return ((b[1] == c and b[2] == c and b[3] == c) or
            (b[4] == c and b[5] == c and b[6] == c) or
            (b[7] == c and b[8] == c and b[9] == c) or
            (b[1] == c and b[4] == c and b[7] == c) or
            (b[2] == c and b[5] == c and b[8] == c) or
            (b[3] == c and b[6] == c and b[9] == c) or
            # for diagonal streak
            (b[7] == c and b[5] == c and b[3] == c) or
            (b[1] == c and b[5] == c and b[9] == c))


def make_move(board, choice, pos):
    """make the move at the given position by the player"""
    board[pos] = choice


def who_goes_first(member_list):
    """randomly choose a player to play first"""

    goes_first = random.choice(member_list)
    return goes_first


def display_board(board):
    """Display the game board to the screen"""
    print(board[7] + '|' + board[8] + '|' + board[9])
    print('-+-+-')
    print(board[4] + '|' + board[5] + '|' + board[6])
    print('-+-+-')
    print(board[1] + '|' + board[2] + '|' + board[3])


def is_space_free(board, pos):
    """Return true or false based on truthy or falsy of space free condition"""

    return board[pos] == ' '


def is_board_full(b):
    """Return true if the board is full and false if not"""

    #assuming all board is full
    is_full = True
    for k in b:
        if is_space_free(b, k):
            is_full = False

    return is_full


def get_player_move(board):
    """Take move input from the players"""

    move = ''
    while move not in '1 2 3 4 5 6 7 8 9'.split() or not is_space_free(board, int(move)):
        move = input('what\'s your move(1-9): ')

    return int(move)


def get_board_copy(board):
    """Return the copy of the board"""
    new_board = {}
    for k in board:
        new_board[k] = board[k]
    return new_board

def choose_random_move_from(board, move_list):
    possible_moves = []
    for k in board:
        if is_space_free(board, k):
            possible_moves.append(k)

    if len(possible_moves) != 0:
        return random.choice(possible_moves)
    else:
        return  None


# move the computer
def get_computer_move(board, computer_choice):
    # check the computer choice
    if computer_choice == 'X':
        player_choice = 'O'
    else:
        player_choice = 'X'


    # check if the next move make it win the game
    for k in board:
        board_copy = get_board_copy(board)
        if is_space_free(board_copy, k):
            make_move(board_copy, computer_choice, k)
            if is_winning(board_copy, computer_choice):
                return k

    # check if the next move make the player win
    for k in board:
        board_copy = get_board_copy(board)
        if is_space_free(board_copy, k):
            make_move(board_copy, player_choice, k)
            if is_winning(board_copy, player_choice):
                return k

    move = choose_random_move_from(board, [1,3,7,9])
    if move != None:
        return move

# take the middle box if it's empty
    if board[5] == ' ':
        return 5

    return choose_random_move_from(board, [2,4,6,8])



def start_game():
    """Game driver code set up the ground work for the game."""

    # create/reset a dictonary of the board with each box as number in keypad
    the_board = {
        1: ' ', 2: ' ', 3: ' ', 4: ' ', 5: ' ',
        6: ' ', 7: ' ', 8: ' ', 9: ' '
    }

    print('Tic Tac Toe'.center(50, '-'))

    user_input = input('\n\nHello! welcome what is your name: ')
    player_name = user_input or 'player'
    active_members = [player_name, 'computer']

    # start of the game loop
    while True:

        # asking player for their choice in 'X' and 'O'
        player_choice, computer_choice = get_choice(player_name)

        turn = who_goes_first(active_members)
        print(f'\nThe {turn} will go first')

        game_is_playing = True

        print(f'\n{player_name}: {player_choice}\ncomputer: {computer_choice}\n')

        # begin the game
        while game_is_playing:
            # check if its player turn
            if turn == player_name:
                # display the game board to  the players
                display_board(the_board)
                print()

                # get player move
                move = get_player_move(the_board)
                make_move(the_board, player_choice, move)

                if is_winning(the_board, player_choice):
                    display_board(the_board)
                    print('Horray! you\'ve won.')
                    game_is_playing = False
                else:
                    if is_board_full(the_board):
                        display_board(the_board)
                        print('The game is a tie.')
                        break
                    else:
                        turn = 'computer'

            # check if its computer turn
            else:

                move = get_computer_move(the_board, computer_choice)
                make_move(the_board, computer_choice, move)

                if is_winning(the_board, computer_choice):
                    display_board(the_board)
                    print('Computer has won! you\'ve lost.')
                    game_is_playing = False
                else:
                    if is_board_full(the_board):
                        display_board(the_board)
                        print('The game is a tie.')
                        break
                    else:
                        turn = player_name

        if not input('Do you want to play again?(yes or no)').lower().startswith('y'):
            break

start_game()
