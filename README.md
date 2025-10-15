# C-Dili-le-Tic-Tac-Toe
C programlama dilinde geliştirilmiş, iki oyunculu, konsol tabanlı basit bir Tic-Tac-Toe oyun uygulaması.

#include <stdio.h>
char board[3][3];

void initialize_board() { 
    int i, j; 
    for (i = 0; i < 3; i++) { 
        for (j = 0; j < 3; j++) { 
            board[i][j] = '-'; 
        } 
    } 
}

void print_board() { 
    int i, j; 
    printf("\n 1 2 3\n"); 
    for (i = 0; i < 3; i++) { 
        printf("%d ", i + 1); 
        for (j = 0; j < 3; j++) { 
            printf("%c ", board[i][j]); 
        } 
        printf("\n"); 
    } 
    printf("\n"); 
}

int player_move(int row, int col, char player) { 
    if (board[row - 1][col - 1] == '-') { 
        board[row - 1][col - 1] = player; 
        return 1; // Geçerli hamle 
    } else { 
        printf("Geçersiz hamle, lütfen tekrar deneyin.\n"); 
        return 0; // Geçersiz hamle 
    } 
}

int check_game_over() { 
    int i, j; 
    // Satırları kontrol et
    for (i = 0; i < 3; i++) { 
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != '-') { 
            return 1; // Kazanan var 
        } 
    } 
    // Sütunları kontrol et
    for (i = 0; i < 3; i++) { 
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != '-') { 
            return 1; // Kazanan var 
        } 
    } 
    // Çaprazları kontrol et
    if ((board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != '-') || (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != '-')) { 
        return 1; // Kazanan var 
    } 
    // Boş yerleri kontrol et (oyun devam ediyor)
    for (i = 0; i < 3; i++) { 
        for (j = 0; j < 3; j++) { 
            if (board[i][j] == '-') { 
                return 0; // Oyun devam ediyor 
            } 
        } 
    } 
    return -1; // Berabere 
}

int main() { 
    int row, col, game_over, valid_move; 
    char player = 'X'; 
    initialize_board(); 
    while (1) { 
        print_board(); 
        printf("Oyuncu %c, satır ve sütun seçin (1-3): ", player);
        
        // Geçerli bir hamle yapılana kadar döngü
        valid_move = 0;
        while (!valid_move) {
            scanf("%d %d", &row, &col);
            if (row < 1 || row > 3 || col < 1 || col > 3) {
                printf("Geçersiz satır veya sütun numarası, lütfen tekrar deneyin.\n");
                continue;
            }
            valid_move = player_move(row, col, player);
        }

        game_over = check_game_over();
        if (game_over == 1) {
            print_board();
            printf("Oyuncu %c kazandı!\n", player);
            break;
        } else if (game_over == -1) {
            print_board();
            printf("Oyun berabere bitti.\n");
            break;
        }

        // Geçerli bir hamleden sonra oyuncu değiştirme
        if (player == 'X') {
            player = 'O';
        } else {
            player = 'X';
        }
    }
    return 0;
}
