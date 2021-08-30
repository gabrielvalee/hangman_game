# Hangman Game in Python

This is the hangman game developed in python for the online course "Python 3 Part 2: Advancing in the language", avaliable in the website "Alura".

In this online course I had to use Python to make a hangman game.

I created 3 .txt files named **"easywords.txt"**, **"mediumwords.txt"** and **"hardwords.txt"**, containing a lot of words in different sizes. The final file is **"hangman.py"**

```python
import random


def run():
    difficulty = select_dificulty()
    secret_word = get_random_word(difficulty)
    revealed_letters = ["_" for nletter in secret_word]
    print_hangman(0)

    total_lifes = 6
    errors = 0

    while (True):
        print_hidden_word(revealed_letters)
        player_letter = get_player_letter()

        if (player_letter in secret_word):  # HIT
            revealed_letters = reveal_letters(secret_word, player_letter, revealed_letters)
            print("The letter {} was found in the word!\n".format(player_letter))
        else:  # MISS
            print("The letter {} wasn't found in the word\n".format(player_letter))
            errors += 1
            print_hangman(errors)
            if (errors == total_lifes):  # GAME OVER
                print_game_over(secret_word)
                break

        if ("_" not in revealed_letters):  # WINNER
            print_win(secret_word)
            break


def print_hangman(step):
    if (step == 0):
        print("**********************************************************************")
        print("****                            ______                            ****")
        print("****                            |/   |                            ****")
        print("****                            |                                 ****")
        print("****                            |                                 ****")
        print("****                            |                                 ****")
        print("****                           /|\\                                ****")
    if (step == 1):
        print("**********************************************************************")
        print("****                            ______                            ****")
        print("****                            |/   |                            ****")
        print("****                            |    O                            ****")
        print("****                            |                                 ****")
        print("****                            |                                 ****")
        print("****                           /|\\                                ****")
    if (step == 2):
        print("**********************************************************************")
        print("****                            ______                            ****")
        print("****                            |/   |                            ****")
        print("****                            |    O                            ****")
        print("****                            |    |                            ****")
        print("****                            |                                 ****")
        print("****                           /|\\                                ****")
    if (step == 3):
        print("**********************************************************************")
        print("****                            ______                            ****")
        print("****                            |/   |                            ****")
        print("****                            |    O                            ****")
        print("****                            |   /|                            ****")
        print("****                            |                                 ****")
        print("****                           /|\\                                ****")
    if (step == 4):
        print("**********************************************************************")
        print("****                            ______                            ****")
        print("****                            |/   |                            ****")
        print("****                            |    O                            ****")
        print("****                            |   /|\\                           ****")
        print("****                            |                                 ****")
        print("****                           /|\\                                ****")
    if (step == 5):
        print("**********************************************************************")
        print("****                            ______                            ****")
        print("****                            |/   |                            ****")
        print("****                            |    O                            ****")
        print("****                            |   /|\\                           ****")
        print("****                            |   /                             ****")
        print("****                           /|\\                                ****")
    if (step == 6):
        print("**********************************************************************")
        print("****                            ______                            ****")
        print("****                            |/   |                            ****")
        print("****                            |    O                            ****")
        print("****                            |   /|\\                           ****")
        print("****                            |   / \\                           ****")
        print("****                           /|\\                                ****")


def select_dificulty():
    print("**********************************************************************")
    print("****                         Hangman Game                         ****")
    print("**********************************************************************")
    print("****                    Choose the difficulty:                    ****")
    print("****                           (1) Easy                           ****")
    print("****                          (2) Medium                          ****")
    print("****                           (3) Hard                           ****")
    print("**********************************************************************")
    difficulty = 0

    while (difficulty not in [1, 2, 3]):  # choosing the difficulty
        difficulty = input("Enter a number between 1 and 3: ")
        if (difficulty == "1" or difficulty == "2" or difficulty == "3"):  # checking user input
            difficulty = int(difficulty)
        else:
            print("Please enter a valid entry!")

    if (difficulty == 1):
        print("**********************************************************************")
        print("****                        You chose easy                        ****")
        print("****            You will have to guess a 5 letter word            ****")
    elif (difficulty == 2):
        print("**********************************************************************")
        print("****                       You chose medium                       ****")
        print("****            You will have to guess a 7 letter word            ****")
    else:
        print("**********************************************************************")
        print("****                        You chose hard                        ****")
        print("****            You will have to guess a 9 letter word            ****")

    return difficulty


def get_random_word(difficulty):
    if (difficulty == 1):
        words_file = open("easywords.txt", "r")  # opening easy file
    elif (difficulty == 2):
        words_file = open("mediumwords.txt", "r")  # opening medium file
    else:
        words_file = open("hardwords.txt", "r")  # opening hard file
    allwords = [file_word.strip() for file_word in words_file]  # getting all the words
    words_file.close()
    secret_word = allwords[random.randrange(0, len(allwords))].lower()  # getting a random word
    return secret_word


def get_player_letter():
    while (True):
        player_letter = input("Insert a letter: ")
        if (not player_letter.isalpha()):
            print("Enter a valid letter!")
            continue
        if (len(player_letter) > 1):
            print("Only enter one letter!")
            continue
        player_letter = player_letter.lower()
        break
    return player_letter


def print_hidden_word(revealed_letters):
    print("**********************************************************************")
    for letter in revealed_letters:
        print("{} ".format(letter), end="")
    print("\n**********************************************************************\n")


def print_game_over(secret_word):
    print("**********************************************************************")
    print("****                          GAME  OVER                          ****")
    print("You lost! The word was \"{}\"".format(secret_word))
    print("**********************************************************************")


def print_win(secret_word):
    print("**********************************************************************")
    print("****                           CONGRATS                           ****")
    print("You won! The word was \"{}\"".format(secret_word))
    print("**********************************************************************")


def reveal_letters(secret_word, player_letter, revealed_letters):
    index = 0
    for word_letter in secret_word:
        if (player_letter == word_letter):
            revealed_letters[index] = player_letter
        index += 1
    return revealed_letters


if(__name__ == "__main__"):
    run()
```

The code will:
 1. Get the the difficult level the player wants.
 2. Open the file then get a random word.
 3. Get the letters with the player and check if the word contains then, until the player wins or loses.
