# Tictactoe
tictactoe where you play a game with AI

def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

def check_win(board, player):
    # Check rows, columns, and diagonals
    for row in board:
        if all([spot == player for spot in row]):
            return True
    for col in range(3):
        if all([board[row][col] == player for row in range(3)]):
            return True
    if all([board[i][i] == player for i in range(3)]) or all([board[i][2 - i] == player for i in range(3)]):
        return True
    return False

def check_draw(board):
    return all([spot != " " for row in board for spot in row])

def get_move(board):
    while True:
        move = input("Enter your move (row and column): ").split()
        if len(move) != 2:
            print("Please enter two numbers.")
            continue
        row, col = move
        if not (row.isdigit() and col.isdigit()):
            print("Please enter valid numbers.")
            continue
        row, col = int(row), int(col)
        if row not in range(3) or col not in range(3):
            print("Please enter numbers between 0 and 2.")
            continue
        if board[row][col] != " ":
            print("That spot is already taken.")
            continue
        return row, col

def play_game():
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"
    while True:
        print_board(board)
        print(f"Player {current_player}'s turn.")
        row, col = get_move(board)
        board[row][col] = current_player
        if check_win(board, current_player):
            print_board(board)
            print(f"Player {current_player} wins!")
            break
        if check_draw(board):
            print_board(board)
            print("The game is a draw!")
            break
        current_player = "O" if current_player == "X" else "X"

if __name__ == "__main__":
    play_game()
