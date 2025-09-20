Simple Brute-Force Password Cracking Algorithm

This project implements a basic algorithm that attempts to guess a user-defined test password using a brute-force method. The goal is to understand the vulnerability of weak passwords and the importance of secure password policies.

The code uses the time library to measure the total execution time of the brute-force process.

import time

Test Password Definition

This section defines the password that the algorithm will attempt to crack. Users can set this password to any desired value.

password = "Ab3!"

Alphabet Definition

Here, the characters used by the algorithm to generate all possible combinations are defined. Separate strings are created for lowercase letters, uppercase letters, numbers, and symbols, which are then combined into a single string.

lowercase = "abcdefghijklmnopqrstuvwxyz"
uppercase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
numbers   = "0123456789"
symbols   = "!@#$%^&*()_+-=[]{}|;':\",./<>?`~ "

alphabet = lowercase + uppercase + numbers + symbols

Counter Initialization

Variables are initialized to track the number of attempts and whether the password has been found.

attempts = 0
found = False

Execution Timer

The starting time is recorded to calculate the total time taken to find the password.

start_time = time.time()

Combination Generation

This is the core of the algorithm, where all possible character combinations are generated and tested. Nested loops iterate over password lengths and character combinations.

for length in range(1, len(password) + 1):
    if found:
        break

    indices = [0] * length
    total_combinations = len(alphabet) ** length

    for num in range(total_combinations):
        attempt = ""
        temp = num

        for i in range(length - 1, -1, -1):
            indices[i] = temp % len(alphabet)
            temp //= len(alphabet)
            attempt += alphabet[indices[i]]

        attempts += 1

Algorithm Explanation

for length in range(1, len(password) + 1):
Iterates over possible password lengths, from 1 to the target password's length. For example, if the password is "Ab3!", the loop will test lengths 1, 2, 3, and 4.

if found:
Checks if the password has already been found. The found variable is set to True when the correct password is discovered.

indices = [0] * length:
Creates a list to store the indices of the alphabet characters for the current combination.

total_combinations = len(alphabet) ** length:
Calculates the total number of possible combinations for the current length.

for num in range(total_combinations):
Iterates over each possible combination number.

attempt = "":
Initializes an empty string to build the password attempt.

temp = num:
Temporary variable used to compute character indices without modifying the loop counter.

for i in range(length - 1, -1, -1):
Builds the password attempt from right to left by converting the numeric value into corresponding alphabet indices.

indices[i] = temp % len(alphabet) and temp //= len(alphabet):
Compute the character index and prepare temp for the next character calculation.

Password Comparison and Output

Each generated combination is compared with the target password. When a match is found, the algorithm prints the result and execution time.

if attempt == password:
    found = True
    end_time = time.time()
    elapsed_time = end_time - start_time
    print(f"Password found: {attempt}")
    print(f"Attempts: {attempts}")
    print(f"Elapsed time: {elapsed_time} seconds")
    break

Example Output

Examples of program output with different passwords:

Password: abc
Password found: abc
Attempts: 17578
Elapsed time: 0.004 seconds

Password: 123
Password found: 123
Attempts: 104768
Elapsed time: 0.005 seconds

Password: Ab3!
Password found: Ab3!
Attempts: 757546
Elapsed time: 0.036 seconds

Reflection

What happens if the password is 8+ characters long and contains uppercase letters, numbers, and symbols?

The number of possible combinations increases exponentially, making it practically impossible to crack with current computational resources. This exercise illustrates the importance of strong passwords and secure policies.
