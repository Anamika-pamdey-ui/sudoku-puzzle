

Sudoku-puzzle 

Introduction

This project is a C-based Sudoku solver that utilizes a backtracking algorithm to find solutions for a given Sudoku puzzle. The program takes an incomplete 9x9 Sudoku grid as input and attempts to fill in the missing numbers while following Sudoku rules.
Example Output

Original puzzle:
3 |   | 9 | 1 |   | 7 |   | 8 | 4 
  | 1 |   |   |   |   | 2 |   |   
7 |   |   | 2 |   | 8 |   |   | 1 
---------------------------------
  | 6 |   |   | 8 |   |   | 4 |   
  |   | 2 |   |   |   | 1 |   |   
  | 3 |   |   | 1 |   |   | 5 |   
---------------------------------
5 |   |   | 8 |   | 6 |   |   | 9 
  |   | 1 |   |   |   | 3 | 7 |   
  | 7 |   | 6 |   | 5 | 8 |   |   

Solved puzzle:
3 | 5 | 8 | 2 | 1 | 6 | 9 | 7 | 4 
4 | 1 | 6 | 9 | 7 | 5 | 2 | 3 | 8 
7 | 2 | 9 | 4 | 3 | 8 | 5 | 6 | 1 
---------------------------------
1 | 6 | 5 | 7 | 8 | 9 | 4 | 2 | 3 
8 | 9 | 2 | 5 | 4 | 3 | 1 | 6 | 7 
2 | 3 | 7 | 6 | 1 | 4 | 8 | 5 | 9 
---------------------------------
5 | 4 | 3 | 8 | 2 | 6 | 7 | 1 | 9 
6 | 8 | 1 | 3 | 9 | 7 | 3 | 7 | 5 
9 | 7 | 4 | 6 | 5 | 2 | 8 | 9 | 2




Features

Solves any valid 9x9 Sudoku puzzle.

Implements a backtracking algorithm for efficient solving.

Displays both the original and solved puzzle in a structured format.


Getting Started

Prerequisites

To compile and run this program, you need:

A C compiler (GCC recommended)

A code editor or terminal

Git (optional, for version control)


Installation

1. Clone the repository:
2. https://github.com/Anamika-pamdey-ui/sudoku-puzzle




How It Works

1. The program reads a 9x9 Sudoku grid, where empty cells are represented by 0.


2. It attempts to fill in the empty cells using a recursive backtracking algorithm.


3. The function valid_move() checks if a number can be placed in a given position without violating Sudoku rules.


4. The solve_puzzle() function attempts numbers from 1 to 9 and proceeds recursively.


5. If a solution is found, it is displayed in a structured format.


FAQS 
For further information, question, answer you can contact me here e-mail anamika.p10902080@gmail.com





//sudoko puzzle using c
#include <stdio.h>

int puzzle[9][9] = {
    {3,0,0,0,2,0,0,7,0},
    {9,0,0,5,0,0,0,1,4},
    {0,1,6,3,7,0,0,0,8},
    {2,0,0,8,0,0,0,0,1},
    {5,0,0,0,4,1,8,0,0},
    {0,8,9,0,0,0,0,5,0},
    {0,0,5,0,1,0,2,8,0},
    {0,4,0,0,0,6,0,9,3},
    {7,3,1,0,8,2,0,0,0}
};

void print_puzzle(int puzzle[9][9]);
int valid_move(int puzzle[9][9], int row, int col, int val);
int solve_puzzle(int puzzle[9][9], int row, int col);

int main() {
    printf("\n\tWelcome to Sudoku solver!!!");
    printf("\n\nOriginal puzzle:");
    print_puzzle(puzzle);

    if (solve_puzzle(puzzle, 0, 0)) {
        printf("\nThe puzzle is solved:");
        print_puzzle(puzzle);
    } else {
        printf("This puzzle is not solved\n");
    }
    
    return 0;
}

int solve_puzzle(int puzzle[9][9], int row, int col) {
    if (col == 9) {
        if (row == 8) {
            return 1; // puzzle solved
        }
        row++;
        col = 0;
    }

    if (puzzle[row][col] > 0) {
        return solve_puzzle(puzzle, row, col + 1);
    }

    for (int i = 1; i <= 9; i++) {
        if (valid_move(puzzle, row, col, i)) {
            puzzle[row][col] = i;
            if (solve_puzzle(puzzle, row, col + 1)) {
                return 1;
            }
            puzzle[row][col] = 0;
        }
    }
    return 0;
}

// valid move check function
int valid_move(int puzzle[9][9], int row, int col, int val) {
    for (int i = 0; i < 9; i++) { // Check row
        if (puzzle[row][i] == val) {
            return 0;
        }
    }
    
    for (int i = 0; i < 9; i++) { // Check column
        if (puzzle[i][col] == val) {
            return 0;
        }
    }
    
    // Check 3x3 subgrid
    int r = row - row % 3;
    int c = col - col % 3;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (puzzle[r + i][c + j] == val) {
                return 0;
            }
        }
    }
    return 1;
}

// Function to print the puzzle
void print_puzzle(int puzzle[9][9]) {
    printf("\n+--------+-------+--------+");
    for (int row = 0; row < 9; row++) {
        printf("\n");
        for (int col = 0; col < 9; col++) {
            if (col % 3 == 0) {
                printf(" |");
            }
            if (puzzle[row][col] != 0) {
                printf(" %d", puzzle[row][col]);
            } else {
                printf("  ");
            }
        }
        printf(" |");
        if ((row + 1) % 3 == 0) {
            printf("\n+--------+-------+--------+");
        }
    }
}
