---
id: cvx36xc7yonzwcwe9viat91
title: 348-tic-tac-toe
desc: ''
updated: 1689317435857
created: 1689305370821
---
## #medium #map #iconic

Assume the following rules are for the tic-tac-toe game on an n x n board between two players:

A move is guaranteed to be valid and is placed on an empty block.
Once a winning condition is reached, no more moves are allowed.
A player who succeeds in placing n of their marks in a horizontal, vertical, or diagonal row wins the game.
Implement the TicTacToe class:

TicTacToe(int n) Initializes the object the size of the board n.
int move(int row, int col, int player) Indicates that the player with id player plays at the cell (row, col) of the board. The move is guaranteed to be a valid move, and the two players alternate in making moves. Return
0 if there is no winner after the move,
1 if player 1 is the winner after the move, or
2 if player 2 is the winner after the move.

## 解题思路

是一个把检测整行整列有没有都画x变为+1, -1正负的思路。这种思路非常常见。由于dia只有一条所以没有用array。

最后记住由于有+1, -1，所以要用Math.abs

class TicTacToe {
    int[] rows;
    int[] cols;
    int dia;
    int antiDia;
    public TicTacToe(int n) {
        rows = new int[n];
        cols = new int[n];
        dia = 0; 
        antiDia = 0;
    }
    
    public int move(int row, int col, int player) {
        int curr = (player == 1) ? 1 : -1;
        int n = rows.length;
        rows[row] += curr;
        cols[col] += curr;
        if (row == col) dia += curr;
        if (col == (n - row - 1)) antiDia+= curr;
        if (Math.abs(rows[row]) == n || Math.abs(cols[col]) == n || Math.abs(dia) == n || Math.abs(antiDia) == n)
            return player;
        return 0;
    }
}

/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe obj = new TicTacToe(n);
 * int param_1 = obj.move(row,col,player);
 */
