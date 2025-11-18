
---

# Tic-Tac-Toe Game (C++)
**Name:** Krish Adiraj  
**Course:** CISC 192 - C++ Programming  
**Assignment:** Tic-Tac-Toe Class Program  
**Due Date:** 11/09/2025  

Objecitve: Write a C++ program that allows two players to play the Tic-Tac-Toe game using a class-based design.
Program Requirements
1. Class Name
TicTacToe --- The class must represent the entire game.

2. Private Members
A 3×3 2D array board[3][3] to store the moves ('X', 'O', or ' ').
Additional variables as needed (e.g., current player, move count, game status).
3. Public Member Functions
void displayBoard() → Print the current game board.\
bool isValidMove(int row, int col) → Check if a move is valid.\
void makeMove(int row, int col) → Place the move on the board.\
bool checkWinner() → Determine if there's a winner.\
bool isDraw() → Check for draw condition.\
void playGame() → Run the full game loop.
4. Gameplay Rules
Player 1 uses 'X', Player 2 uses 'O'.
Players take turns entering row and column numbers (1--3).
After each move, the board updates and the winner/draw is checked
---

## 📘 Program Description
This program lets two players play Tic-Tac-Toe using a **class-based design**.  
The game uses a `TicTacToe` class that stores the board, current player, and game logic.

Players enter row and column numbers (1–3), and the board updates until either:
- A player wins, or  
- The game ends in a draw  

---

## C++ Source Code

```cpp
#include <iostream>
using namespace std;

// TicTacToe class handles the entire game
class TicTacToe {
private:
    char board[3][3];
    char currentPlayer;
    int moveCount;

public:
    // Constructor initializes the board and starting player
    TicTacToe() {
        currentPlayer = 'X';
        moveCount = 0;

        // Start with empty spaces
        for (int r = 0; r < 3; r++) {
            for (int c = 0; c < 3; c++) {
                board[r][c] = ' ';
            }
        }
    }

    // Displays the current board
    void displayBoard() {
        cout << "\n  1   2   3\n";
        for (int r = 0; r < 3; r++) {
            cout << r + 1 << " ";
            for (int c = 0; c < 3; c++) {
                cout << board[r][c];
                if (c < 2) cout << " | ";
            }
            cout << "\n";
            if (r < 2) cout << " ---+---+---\n";
        }
        cout << endl;
    }

    // Checks if the player's move is valid
    bool isValidMove(int row, int col) {
        return (row >= 0 && row < 3 &&
                col >= 0 && col < 3 &&
                board[row][col] == ' ');
    }

    // Places the move on the board
    void makeMove(int row, int col) {
        board[row][col] = currentPlayer;
        moveCount++;
    }

    // Checks for a winner (rows, columns, diagonals)
    bool checkWinner() {
        // Check rows and columns
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == currentPlayer &&
                board[i][1] == currentPlayer &&
                board[i][2] == currentPlayer)
                return true;

            if (board[0][i] == currentPlayer &&
                board[1][i] == currentPlayer &&
                board[2][i] == currentPlayer)
                return true;
        }

        // Main diagonal
        if (board[0][0] == currentPlayer &&
            board[1][1] == currentPlayer &&
            board[2][2] == currentPlayer)
            return true;

        // Other diagonal
        if (board[0][2] == currentPlayer &&
            board[1][1] == currentPlayer &&
            board[2][0] == currentPlayer)
            return true;

        return false;
    }

    // Checks for draw
    bool isDraw() {
        return moveCount == 9;
    }

    // Switch players
    void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    // Runs the main game loop
    void playGame() {
        cout << "Welcome to Tic-Tac-Toe!\n";
        displayBoard();

        while (true) {
            int row, col;

            cout << "Player " << currentPlayer << ", enter row (1-3): ";
            cin >> row;
            cout << "Enter column (1-3): ";
            cin >> col;

            // Convert to index
            row--;
            col--;

            if (!isValidMove(row, col)) {
                cout << "Invalid move. Try again.\n";
                continue;
            }

            makeMove(row, col);
            displayBoard();

            if (checkWinner()) {
                cout << "Player " << currentPlayer << " wins!\n";
                break;
            }

            if (isDraw()) {
                cout << "The game is a draw.\n";
                break;
            }

            switchPlayer();
        }
    }
};

int main() {
    TicTacToe game;
    game.playGame();
    return 0;
}
