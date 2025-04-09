#include <stdio.h>

char board[3][3]; 
void initializeBoard() {
    char value = '1';
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = value++;
        }
    }
}
void printBoard() {
    printf("\nTic-Tac-Toe Board:\n\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf(" %c ", board[i][j]);
            if (j < 2) printf("|");
        }
        printf("\n");
        if (i < 2) printf("---|---|---\n");
    }
    printf("\n");
}
int checkWin() {
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) return 1;
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) return 1;
    }
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) return 1;
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) return 1;

    return 0;
}
int isBoardFull() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] != 'X' && board[i][j] != 'O') {
                return 0; 
            }
        }
    }
    return 1;
}
void playGame() {
    int player = 1; 
    int choice;
    int row, col;
    char mark;

    while (1) {
        printBoard();
        printf("Player %d, enter a number (1-9): ", player);
        scanf("%d", &choice);
        row = (choice - 1) / 3;
        col = (choice - 1) % 3;
        if (board[row][col] == 'X' || board[row][col] == 'O') {
            printf("Cell already taken, try again.\n");
            continue;
        }
        mark = (player == 1) ? 'X' : 'O';
        board[row][col] = mark;

        if (checkWin()) {
            printBoard();
            printf("Player %d wins!\n", player);
            break;
        }
        if (isBoardFull()) {
            printBoard();
            printf("It's a tie!\n");
            break;
        }
        player = (player == 1) ? 2 : 1;
    }
}

int main() {
    initializeBoard();
    playGame();
    return 0;
}
