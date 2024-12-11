#include <stdio.h>
#include <stdlib.h>
#include <time.h>


void toss();
int playerBatting(int target);
int computerBatting(int target);

int main() {
    int playerScore = 0, computerScore = 0;
    int tossResult, playerChoice;
    int firstInningDone = 0;

    srand(time(0));

    printf("Welcome to the AMUST CRICKET GAME!\n");
    printf(" Here Are The Rules:\n");
    printf("1. Toss decides who bats or bowls first.\n");
    printf("2. One-over (6 balls) and one wicket game.\n");
    printf("3. Guess the machine's run to get it out.\n");
    printf("\n");

    printf("Let's do the toss! Call 1 for Heads or 2 for Tails: ");
    scanf("%d", &playerChoice);

    tossResult = (rand() % 2) + 1;
    if (tossResult == playerChoice) {
        printf("You won the toss! Choose:\n1. Bat\n2. Bowl\n");
        scanf("%d", &playerChoice);
    } else {
        printf("Computer won the toss! ");
        playerChoice = (rand() % 2) + 1;
        if (playerChoice == 1) {
            printf("Computer chooses to bat first.\n");
        } else {
            printf("Computer chooses to bowl first.\n");
        }
    }
     if (playerChoice == 1) {
        printf("\nPlayer is batting first...\n");
        playerScore = playerBatting(0);
        printf("\nComputer needs to chase %d to win.\n", playerScore + 1);
        computerScore = computerBatting(playerScore);
    } else {
        printf("\nComputer is batting first...\n");
        computerScore = computerBatting(0);
        printf("\nPlayer needs to chase %d to win.\n", computerScore + 1);
        playerScore = playerBatting(computerScore);
    }

    if (playerScore > computerScore) {
        printf("\nPlayer wins by %d runs!\n", playerScore - computerScore);
    } else if (computerScore > playerScore) {
        printf("\nComputer wins by %d runs!\n", computerScore - playerScore);
    } else {
        printf("\nIt's a tie!\n");
    }

    return 0;
}
int playerBatting(int target) {
    int score = 0, playerInput, computerInput, balls = 6;

    while (balls > 0) {
        printf("\nEnter your run (1-6): ");
        scanf("%d", &playerInput);

        if (playerInput < 1 || playerInput > 6) {
            printf("Invalid input! Please enter a number between 1 and 6.\n");
            continue;
        }

        computerInput = (rand() % 6) + 1;
        printf("Computer bowls: %d\n", computerInput);

        if (playerInput == computerInput) {
            printf("Out! You scored %d runs.\n", score);
            break;
        }

        score += playerInput;
        printf("Your score: %d\n", score);
        balls--;

        if (target > 0 && score > target) {
            printf("You've chased the target successfully!\n");
            break;
        }
    }

    return score;
}
int computerBatting(int target) {
    int score = 0, playerInput, computerInput, balls = 6;

    while (balls > 0) {
        printf("\nGuess the computer's run (1-6): ");
        scanf("%d", &playerInput);

        if (playerInput < 1 || playerInput > 6) {
            printf("Invalid input! Please enter a number between 1 and 6.\n");
            continue;
        }

        computerInput = (rand() % 6) + 1;
        printf("Computer bats: %d\n", computerInput);

        if (playerInput == computerInput) {
            printf("Out! Computer scored %d runs.\n", score);
            break;
        }

        score += computerInput;
        printf("Computer's score: %d\n", score);
        balls--;

        if (target > 0 && score > target) {
            printf("Computer has chased the target successfully!\n");
            break;
        }
    }

    return score;
}
