def print_board(board):
    print("\n")
    for row in board:
        print(" | ".join(row))
        print("-" * 9)
    print("\n")

def check_win(board, player):
    # Rows, Columns, Diagonals
    for row in board:
        if all(cell == player for cell in row):
            return True
    
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    
    if all(board[i][i] == player for i in range(3)):
        return True
    
    if all(board[i][2 - i] == player for i in range(3)):
        return True
    
    return False

def check_draw(board):
    return all(cell in ["X", "O"] for row in board for cell in row)

def play_game():
    board = [["1", "2", "3"],
             ["4", "5", "6"],
             ["7", "8", "9"]]
    
    current_player = "X"
    
    while True:
        print_board(board)
        move = input(f"Player {current_player}, enter a number (1-9): ")

        # Validate input
        if not move.isdigit() or int(move) < 1 or int(move) > 9:
            print("Invalid input. Try again.")
            continue

        move = int(move) - 1
        row, col = move // 3, move % 3

        if board[row][col] in ["X", "O"]:
            print("Cell already taken. Try another move.")
            continue

        board[row][col] = current_player

        if check_win(board, current_player):
            print_board(board)
            print(f"🎉 Player {current_player} wins!")
            break

        if check_draw(board):
            print_board(board)
            print("It's a draw!")
            break

        # Switch players
        current_player = "O" if current_player == "X" else "X"

while True:
    play_game()
    again = input("Play again? (y/n): ")
    if again.lower() != 'y':
        print("Thanks for playing!")
        break
