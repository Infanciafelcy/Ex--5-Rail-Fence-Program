# Ex--5-Rail-Fence-Program
## Name: Infancia Felcy P
## Reg no: 212223040067
# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
def encrypt_rail_fence(text, rails):
    # Create the Rail Fence pattern
    rail = [['\n' for _ in range(len(text))] for _ in range(rails)]

    row, down = 0, False
    for i, char in enumerate(text):
        rail[row][i] = char
        if row == 0 or row == rails - 1:
            down = not down
        row += 1 if down else -1

    # Read the encrypted text row-wise
    cipher = []
    for r in rail:
        cipher.extend([c for c in r if c != '\n'])

    return "".join(cipher)


def decrypt_rail_fence(cipher, rails):
    # Create the Rail Fence matrix
    rail = [['\n' for _ in range(len(cipher))] for _ in range(rails)]

    # Mark positions with '*'
    row, down = 0, False
    for i in range(len(cipher)):
        rail[row][i] = '*'
        if row == 0 or row == rails - 1:
            down = not down
        row += 1 if down else -1

    # Fill the marked positions with cipher characters
    index = 0
    for r in range(rails):
        for c in range(len(cipher)):
            if rail[r][c] == '*' and index < len(cipher):
                rail[r][c] = cipher[index]
                index += 1

    # Read the matrix in zig-zag order
    result = []
    row, down = 0, False
    for i in range(len(cipher)):
        result.append(rail[row][i])
        if row == 0 or row == rails - 1:
            down = not down
        row += 1 if down else -1

    return "".join(result)


# Get user input
plain_text = input("Enter the text to encrypt: ")
rails = int(input("Enter the number of rails: "))

# Encrypt and decrypt
encrypted_text = encrypt_rail_fence(plain_text, rails)
print("\nEncrypted:", encrypted_text)

decrypted_text = decrypt_rail_fence(encrypted_text, rails)
print("Decrypted:", decrypted_text)

# OUTPUT
![image](https://github.com/user-attachments/assets/261c6ed0-1b17-459d-9625-580b0b8a80fd)

# RESULT
The code executed successfully!
