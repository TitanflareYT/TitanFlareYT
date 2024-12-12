import random
import time

# Colorful text helper functions
def print_welcome_message():
    print("\033[1;32mWelcome to the Interactive Number Guessing Game!\033[0m")
    print("\033[1;34mCan you guess the number I am thinking of?\033[0m")
    print("\033[1;33mLet's see if you can do it in as few attempts as possible!\033[0m")

def print_instructions():
    print("\033[1;36mI will pick a random number between a certain range depending on the difficulty level.\033[0m")
    print("\033[1;36mYou’ll need to guess it as quickly as possible. Let's start!\033[0m")

def print_game_over():
    print("\033[1;31mGame Over! Better luck next time!\033[0m")

def print_congratulations(attempts, level):
    print(f"\033[1;32mGreat job! You guessed it in {attempts} attempts!\033[0m")
    print(f"\033[1;33mYou played on {level} difficulty!\033[0m")
    
# Difficulty options
def choose_difficulty():
    print("\033[1;35mChoose a difficulty level:\033[0m")
    print("\033[1;36m1. Easy: Numbers between 1 and 50\033[0m")
    print("\033[1;36m2. Medium: Numbers between 1 and 100\033[0m")
    print("\033[1;36m3. Hard: Numbers between 1 and 200\033[0m")
    
    while True:
        try:
            choice = int(input("\033[1;37mEnter 1, 2, or 3 for your choice: \033[0m"))
            if choice == 1:
                return 50
            elif choice == 2:
                return 100
            elif choice == 3:
                return 200
            else:
                print("\033[1;31mPlease choose a valid difficulty (1, 2, or 3).\033[0m")
        except ValueError:
            print("\033[1;31mPlease enter a valid number.\033[0m")

# Main game function
def guess_the_number():
    print_welcome_message()
    print_instructions()
    
    # Choose difficulty
    max_number = choose_difficulty()
    secret_number = random.randint(1, max_number)
    
    attempts = 0
    start_time = time.time()  # Start the timer
    
    print(f"\033[1;37mI’ve chosen a number between 1 and {max_number}!\033[0m")
    print("\033[1;36mStart guessing!\033[0m")
    
    while True:
        try:
            # Get user input
            guess = int(input("\033[1;37mYour guess: \033[0m"))
            attempts += 1

            # Check guess
            if guess < secret_number:
                print("\033[1;33mToo low! Try again!\033[0m")
            elif guess > secret_number:
                print("\033[1;33mToo high! Try again!\033[0m")
            else:
                # When correct guess is made
                end_time = time.time()  # Stop the timer
                elapsed_time = round(end_time - start_time, 2)
                print_congratulations(attempts, "Easy" if max_number == 50 else "Medium" if max_number == 100 else "Hard")
                print(f"\033[1;32mIt took you {elapsed_time} seconds to guess correctly.\033[0m")
                break
        except ValueError:
            print("\033[1;31mPlease enter a valid number.\033[0m")
    
# Run the game
if __name__ == "__main__":
    guess_the_number()


