- 👋 Hi, I'm @kyaaaaaaa
- 👀 I am interested in programming and information systems
- 🌱 I am currently studying at the university
💞 ️ ́ I am looking for opportunities to collaborate with different people to improve my knowledge
- 📫 How to contact me t.asylbek98@gmail.com

My first code for the console game "Sea Battle" is written in C, developed by a group of 3 people, and with the help of a teacher.

#include <stdio.h> // I/O header file
#include <stdlib.h> // Header file of the C standard library, which contains functions, memory, program execution, type conversion.
#include <string.h> // Header file of the C standard library containing functions for working with strings ending in 0 and various memory functions
#include <ctype.h> // Header file of the C programming language standard library containing function declarations for classifying and converting individual characters
#include <time.h> // Header file of the C programming language standard library containing types and functions for working with date and time.

// Macros for the number of rows and columns on the playing field
#define rows 10
#define cols 10

// Function for displaying the playing field
void print_field(char field[rows][cols]) {
printf(" 1 2 3 4 5 6 7 8 9 10\ n"); // Column header
    printf(" ----------------------\ n"); // Dividing line

// Output of lines of the playing field
    for (int i = 0; i < rows; i++) {
printf("%c |", 'A' + i); // Print the letter of the string
        for (int j = 0; j < cols; j++) {
printf("%c ", field[i][j]); // Printing the symbol of the game cell
        }
printf("|\n"); // End of line
    }
printf(" ----------------------\ n"); // Dividing line
}

// The main function of the program
int main() {
char player_field[rows][cols]; // The playing field for the player
    char computer_field[rows][cols]; // Computer playing field
    int player_ships = 5; // Number of player ships
    int computer_ships = 5; // Number of computer ships
    char player_name[20];
    printf("Welcome to the game \"Sea Battle\"!\n");
    printf("Briefly about the rules of the game: You need to shoot at enemy ships using coordinates. The winner is the one who kills all the enemy ships!\n"); 
    printf("Players take turns, the size of the playing field is only 10x10, you have only 5 ships, and you need to arrange them as you want!\n");
    printf("The coordinates and placement of ships are entered only in English!\n");
    printf("Players can only walk in the playing field, going outside the field is impossible.\n");
    printf("To start walking, you need to enter the coordinates of the playing field, (for example J1)\n");
    printf("Have fun with the game, and I wish you good luck!\n");
    printf("Enter your name: ");
    scanf("%s", player_name);
    printf ("Welcome, %s! I think it's time for you to arrange your ships, because the game will start soon.\n", player_name);

// Initializing the playing fields
    for (int i = 0; i < rows; i++) {
for (int j = 0; j < cols; j++) {
player_field[i][j] = '.'; // Player's playing field
            computer_field[i][j] = '.'; // Computer's playing field
        }
    }

// We arrange the player's ships
    printf("Place your ships on the playing field:\n");
    int x, y;
    for (int i = 0; i < player_ships; i++) {
printf("Ship %d:\n", i + 1);
    do {
        printf("Enter the coordinates of the initial cell: ");
        scanf(" %c%d", &x, &y); // Reading coordinates
        x = tolower(x) - 'a'; // Convert the letter of the string to a number
        y -= 1; // Subtract 1 to get the column index
    } while (x < 0 || x >= rows || y < 0 || y >= cols || player_field[x][y] != '.');
    player_field[x][y] = 'O'; // Marking the cell where the ship
is }

// Placing the computer's ships (randomly)
printf("The computer places its ships randomly on the playing field \n");
    srand(time(NULL)); // Initializing the random number generator
    for (int i = 0; i < computer_ships; i++) {
        do {
            x = rand() %rows; // Random string
            y = rand() %cols; // Random column
        } while (computer_field[x][y] != '.');
        computer_field[x][y] = 'O'; // Marking the cell where the ship is
    }

// Main Game cycle
    while (player_ships > 0 && computer_ships > 0) {
// Player's move
        printf("\Your move:\n");
        print_field(computer_field); // Output the computer's playing field
        do {
            printf("Enter the coordinates of the target: ");
            scanf(" %c%d", &x, &y); // Reading coordinates
            x = tolower(x) - 'a'; // Convert the letter of the string to a number
            y -= 1; // Subtract 1 to get the column index
        } while (x < 0 || x >= rows || y < 0 || y >= cols || computer_field[x][y] == 'X' || computer_field[x][y] == '*');
        if (computer_field[x][y] == 'O') {
            printf("You got it!\n");
            computer_field[x][y] = 'X'; // Marking a hit on the computer field
            computer_ships--;
        } else {
            printf("You didn't hit it.\n");
            computer_field[x][y] = '*'; // Marking a miss on the computer field
    }
if (computer_ships == 0) break; // If the computer has no ships left, the game ends

// Computer running (random)
printf("\Computer running:\n");
    do {
        x = rand() %rows; // Random string
        y = rand() %cols; // Random column
    } while (player_field[x][y] == 'X' || player_field[x][y] == '*');
    if (player_field[x][y] == 'O') {
printf("Computer hit!\n");
        player_field[x][y] = 'X'; // Marking a hit on the player's field
        player_ships--;
    } else {
        printf("The computer did not hit.\n");
        player_field[x][y] = '*'; // Marking a miss on the player's field
    }
}

// The game is over
    printf("\The frame is completed! ");
    if (player_ships == 0) {
        printf("You've lost.\n");
    } else {
        printf("You've won!\n");
    }

  // Output the final state of the playing fields
  printf("Your playing field:\n");
  print_field(player_field);
  printf("Computer playing field:\n");
  print_field(computer_field);

  return 0;
}
