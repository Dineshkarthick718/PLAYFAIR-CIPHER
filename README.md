## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




## Program:
```
def key_matrix(key):
    key = key.upper().replace("J", "I")
    s = ""
    for ch in key + "ABCDEFGHIKLMNOPQRSTUVWXYZ":
        if ch.isalpha() and ch not in s:
            s += ch
    return [list(s[i:i+5]) for i in range(0, 25, 5)]

def pos(mat, ch):
    if ch == "J":
        ch = "I"
    for i in range(5):
        for j in range(5):
            if mat[i][j] == ch:
                return i, j

def encrypt(text, mat):
    text = text.upper().replace("J", "I").replace(" ", "")
    if len(text) % 2 != 0:
        text += "X"
    cipher = ""
    for i in range(0, len(text), 2):
        r1, c1 = pos(mat, text[i])
        r2, c2 = pos(mat, text[i + 1])
        if r1 == r2:
            cipher += mat[r1][(c1 + 1) % 5] + mat[r2][(c2 + 1) % 5]
        elif c1 == c2:
            cipher += mat[(r1 + 1) % 5][c1] + mat[(r2 + 1) % 5][c2]
        else:
            cipher += mat[r1][c2] + mat[r2][c1]
    return cipher

key = input("Enter key: ")
plain = input("Enter plain text: ")

matrix = key_matrix(key)

print("\nPlayfair Key Matrix:")
for row in matrix:
    print(" ".join(row))

print("\nEncrypted Message:", encrypt(plain, matrix))
```

## OUTPUT:
<img width="421" height="321" alt="image" src="https://github.com/user-attachments/assets/2bbe65d6-e5fb-418f-ab57-39d50e3bdbcb" />


## RESULT:
Thus the implementation of playfiar cipher had been executed successfully.





Output:
