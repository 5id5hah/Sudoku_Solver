# 🎯 Sudoku Solver in Java

Welcome to the **Sudoku Solver**! 🧩 This Java program helps you solve any 9x9 Sudoku puzzle using a backtracking algorithm.

## 📋 How It Works

The Sudoku puzzle is represented by a 9x9 grid, where:
- Numbers `1-9` represent filled cells.
- `0` represents an empty cell.

The program recursively fills the grid by placing numbers in empty cells, ensuring that:
- Each number appears only once per row.
- Each number appears only once per column.
- Each number appears only once per 3x3 subgrid.

## 🚀 Getting Started

public class Sudoku {
    public static void main(String[] args) {
        int[][] board = {  {7, 0, 0, 0, 0, 0, 2, 0, 0},
                {4, 0, 2, 0, 0, 0, 0, 0, 3},
                {0, 0, 0, 2, 0, 1, 0, 0, 0},
                {3, 0, 0, 1, 8, 0, 0, 9, 7},
                {0, 0, 9, 0, 7, 0, 6, 0, 0},
                {6, 5, 0, 0, 3, 2, 0, 0, 1},
                {0, 0, 0, 4, 0, 9, 0, 0, 0},
                {5, 0, 0, 0, 0, 0, 1, 0, 6},
                {0, 0, 6, 0, 0, 0, 0, 0, 8}
        };
        if(Solver(board)){
            Display(board);
        }else {
            System.out.println("Cannot solve the sudoku");
        }
    }
    static boolean Solver(int[][] board){
        int n = board.length;;
        int row = -1;
        int col = -1;
        boolean isEmpty = true;
        // this is how we replace c,r in arguments
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 0){
                    row = i;
                    col = j;
                    isEmpty = false;
                    break;
                }
            }
            //if some element is found in the row, just break
            if (isEmpty == false){
            break;
            }
        }
        if (isEmpty == true){
            return true;
            //sudoku is solved
        }
        //now backtrack
        for (int number = 1; number <= 9; number++) {
            if (isSafe(board,row,col,number)){
                board[row][col] = number;
                if (Solver(board)){
                    //answer is found

                    return true;
                }else {
                    //backtrack i.e replace the changes
                    board[row][col] = 0;
                }
            }
        }
        return false;
    }
    static void Display(int[][] board){
        for (int[] row : board){
            for (int number : row){
                System.out.print(number+" ");
            }
            System.out.println();
        }
    }
    static boolean isSafe(int[][] board, int row, int col, int num){
        //check row
        for (int i = 0; i < board.length; i++) {
            //check if the number is already present
            if (board[row][col] == num){
                return false;
            }
        }
        //check col
        for (int[] nums :board) {
            //check if the number is already present
            if (nums[col] == num){
                return false;
            }
        }
        int sqrt = (int)(Math.sqrt(board.length));
        int rowstart = row - (row%sqrt);
        int colstart = col - (col%sqrt);
        for (int r = rowstart; r < rowstart+sqrt; r++) {
            for (int c = colstart; c < colstart+sqrt; c++) {
                if (board[r][c] == num){
                    return false;
                }
            }
        }
        return true;
    }
}

