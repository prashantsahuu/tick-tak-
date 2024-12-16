import java.util.Scanner;
public class Main {
            private static char[][] board = {
                    {' ', ' ', ' '},
                    {' ', ' ', ' '},
                    {' ', ' ', ' '}
            };
            private static char currentPlayer = 'X';

            public static void main(String[] args) {
                System.out.println("Welcome to Tic-Tac-Toe!");
                printBoard();

                while (true) {
                    playerMove();
                    printBoard();

                    if (checkWin()) {
                        System.out.println("Player " + currentPlayer + " wins!");
                        break;
                    } else if (isBoardFull()) {
                        System.out.println("The game is a draw!");
                        break;
                    }

                    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
                }
            }

            private static void printBoard() {
                System.out.println("  0 1 2");
                for (int i = 0; i < 3; i++) {
                    System.out.print(i + " ");
                    for (int j = 0; j < 3; j++) {
                        System.out.print(board[i][j]);
                        if (j < 2) System.out.print("|");
                    }
                    System.out.println();
                    if (i < 2) System.out.println("  -----");
                }
            }

            private static void playerMove() {
                Scanner scanner = new Scanner(System.in);
                int row, col;

                while (true) {
                    System.out.println("Player " + currentPlayer + ", enter your move (row and column): ");
                    row = scanner.nextInt();
                    col = scanner.nextInt();

                    if (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ') {
                        board[row][col] = currentPlayer;
                        break;
                    } else {
                        System.out.println("This move is not valid. Try again.");
                    }
                }
            }

            private static boolean checkWin() {
                // Check rows and columns
                for (int i = 0; i < 3; i++) {
                    if ((board[i][0] == currentPlayer && board[i][1] == currentPlayer && board[i][2] == currentPlayer) ||
                            (board[0][i] == currentPlayer && board[1][i] == currentPlayer && board[2][i] == currentPlayer)) {
                        return true;
                    }
                }

                // Check diagonals
                if ((board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer) ||
                        (board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer)) {
                    return true;
                }

                return false;
            }

            private static boolean isBoardFull() {
                for (int i = 0; i < 3; i++) {
                    for (int j = 0; j < 3; j++) {
                        if (board[i][j] == ' ') {
                            return false;
                        }
                    }
                }
                return true;
            }
        }
