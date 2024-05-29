

Simplifying Boolean Expressions Using the Quine-McCluskey Method

Abstract

This project aims to develop a Python implementation of the Quine-McCluskey (QM) method for simplifying Boolean expressions. The project focuses on the simplicity and clarity of the algorithm while providing a robust solution for generating prime implicants and minimising Boolean expressions using Petrick's Method. The implementation can be further optimised for performance. The algorithm comprises two main parts: generating prime implicants by recursively performing a 1-bit comparison, and selecting the minimum set of prime implicants that cover all minterms using Petrick's Method.

Introduction

Boolean expressions are fundamental in digital logic design and simplifying them is essential for creating efficient logic circuits. The Quine-McCluskey method is a systematic approach for minimising Boolean functions, which is especially useful for functions with many variables. This project implements the QM method in Python, including an explanation of the algorithm and a complete code implementation.

1. Implementation


Algorithm for the Quine-McCluskey Method

Step-by-Step Explanation
(Note: Italic font has been used to show the code snippets)

1. Collect All Minterms
   Convert each minterm to its binary representation.
   Store these binary representations in a list (`Minterm_List`).

   Example:
   minterms = [2, 4, 6, 7, 8]
   binary_minterms = ['0010', '0100', '0110', '0111', '1000']

2. Initialise Lists
   Create `List_1` by copying the minterm list and removing duplicates.

   Example:
   List_1 = ['0010', '0100', '0110', '0111', '1000']

3. Process Don't Care Terms (if any)
   Convert don’t care terms to binary and add to `List_1`.

   Example:
   dont_care_terms = [3, 5]
   List_1 += ['0011', '0101']

4. 1-Bit Comparison and Grouping
   Compare each binary string in `List_1` with every other string.
   If they differ by exactly one bit, create a new string with a wildcard `_` at the    differing bit position and add to `List_2`.
   If no such comparison is possible, add the string to `List_3`.

   Example:
   List_2 = ['0_10', '01_0']
   List_3 = ['1000', '0110']

5. Iterate Until Completion
   Repeat the above steps until `List_1` and `List_2` are empty.
   The final `List_3` will contain all prime implicants.

   Example:
   List_3 = ['1000', '0_10', '011_', '01_0']

6. Remove Duplicates from List_3
   Convert `List_3` to a set to remove duplicates and convert it back to a list.

   Example:
   List_3 = list(set(List_3))

7. Create Prime Implicant Table
   For each prime implicant, determine the minterms it covers by replacing wildcards with all possible 0 and 1 combinations.

   Example:
   Table: 
          Implicant     Implicant_string           Combo           Binrep
0            I0                  0001                      [m8]             1000
1            I1                  0010                  [m2, m6]           0_10
2            I2                  0100                  [m6, m7]           011_
3            I3                 1000                   [m4, m6]          01_0

8. Apply Petrick's Method
   Construct a logical function \( P \) that represents all columns being covered.
   Use De Morgan's Laws to simplify \( P \) into a sum of products.
   Identify the minimum set of prime implicants by finding the terms with the fewest literals.

   Example:
   P = (I0 + I1) * (I1 + I2) * (I2 + I3)
   Simplified P = I1I2 + I0I3

9. Generate Simplified Boolean Expression
   Convert the selected prime implicants back to the original Boolean variables.

   Example:
   Expression = A'B + BC

Python Code Implementation

The full Python code for the QM method can be found at below provided link. It includes functions for cleaning input strings, generating binary representations, performing 1-bit comparisons, and applying Petrick's method to find the minimal Boolean expression. 

Link for code:     https://colab.research.google.com/drive/1VF64CmS8yDI9CVR1CmkIuO5YvhfrG4hN



2. Results  
(a) Generate minterms based on your uppercase first name's ASCII code. Treat each digit of the ASCII code as a minterm. If any digit is repeated, consider it only once. Use the generated minterms to obtain the minimized SOP expression (using the Quine-McCluskey method). 

[Note: input part of the code has been underlined]

Do you want to provide your name or SoP implicants?
choose 'y' for name and 'n' for SoP implicants: y

please type your first name: RISHIKESH

Corresponding min-term input for the name is: [82, 73, 83, 72, 73, 75, 69, 83, 72]
Do you know the number of variables for your equation?
Type 'y' for yes and 'n' for no: n


The least number of variable based on your input is: 7

Number of variable in the expression is: 7 , from a to g

The binary representation of all the given minterms is:  ['1000101', '1001000', '1001001', '1001011', '1010010', '1010011']
List after recursively running the 1 bit difference is:  ['101001_', '1000101', '100100_', '10010_1']
List_final is: ['101001_', '1000101', '100100_', '10010_1']

List_2 containing all the minterms, except don't care is: 
['m69', 'm72', 'm73', 'm75', 'm82', 'm83']

df7 is a table formed from List_final
It is a table containing columns as: Implicant, Implicant_string, Combo, Binrep
Implicant is just a serialisation of implicants
Implicant_string is another way of serialising the implicants, so that tabular method of Petric's method can be implemented
Combo gives the list of minterm(excluding don't care) which are grouped together to form that implicant
Binrep gives the binary representation of that implicant

df7 is:
   Implicant   Implicant_string       Combo                  Binrep
0        I0             0001               [m82, m83]              101001_
1        I1             0010                  [m69]                    1000101
2        I2             0100               [m72, m73]              100100_
3        I3             1000               [m73, m75]               10010_1

Dict_1 is a dictionary whose keys corresponds to the minterm and values in that
key corresponds to the implicant which contains those minterm.
Dict_1 is:
 {'m69': ['0010'], 'm72': ['0100'], 'm73': ['0100', '1000'], 'm75': ['1000'], 'm82': ['0001'], 'm83': ['0001']}

final_list_old gives you the list of implicants which covers all the minterms
final_list_old is: ['1111']
df9 is a table created by final_list_old, which arranges the implicants
df9 is:
              Group Binrep  num_term
0  [I3, I2, I1, I0]   1111         4

Your expression 1 is:
['I3', 'I2', 'I1', 'I0']
ab'c'de'g + ab'c'de'f' + ab'c'd'ef'g + ab'cd'e'f 



(a) Generate minterms based on your uppercase first name's ASCII code. Treat each digit of the ASCII code as a minterm. If any digit is repeated, consider it only once. Use the generated minterms to obtain the minimized SOP expression (using the Quine-McCluskey method). 

[Note: input part of the code has been underlined]

Do you want to provide your name or SoP implicants?
choose 'y' for name and 'n' for SoP implicants: n
please provide your input with SoP implicants in comma separated format
0,5,7,8,9,12,13,23,24,25,28,29,37,40,42,44,46,55,56,57,60,61

Do you want to provide don't care for your expression?

choose 'y' for yes and 'n' for no: n

Given min-term input is: 0,5,7,8,9,12,13,23,24,25,28,29,37,40,42,44,46,55,56,57,60,61

Given don't care min-term input is: 


Do you know the number of variables for your equation?
Type 'y' for yes and 'n' for no: n


The least number of variable based on your input is: 6

Number of variable in the expression is: 6 , from a to f

The binary representation of all the given minterms is:  ['000000', '000101', '000111', '001000', '001001', '001100', '001101', '010111', '011000', '011001', '011100', '011101', '100101', '101000', '101010', '101100', '101110', '110111', '111000', '111001', '111100', '111101']
List after recursively running the 1 bit difference is:  ['0001_1', '101__0', '00_000', '__1_00', '00_101', '_11_0_', '0_0111', '0_1_0_', '_10111', '_00101']
List_final is: ['0001_1', '101__0', '00_000', '__1_00', '00_101', '_11_0_', '0_0111', '0_1_0_', '_10111', '_00101']

List_2 containing all the minterms, except don't care is:  ['m0', 'm5', 'm7', 'm8', 'm9', 'm12', 'm13', 'm23', 'm24', 'm25', 'm28', 'm29', 'm37', 'm40', 'm42', 'm44', 'm46', 'm55', 'm56', 'm57', 'm60', 'm61']
df7 is a table formed from List_final
It is a table containing columns as: Implicant, Implicant_string, Combo, Binrep
Implicant is just a serialisation of implicants
Implicant_string is another way of serialising the implicants, so that tabular method of Petric's method can be implemented
Combo gives the list of minterm(excluding don't care) which are grouped together to form that implicant
Binrep gives the binary representation of that implicant

df7 is:
   Implicant   Implicant_string                                     Combo                                Binrep
0        I0         0000000001   [m8, m12, m24, m28, m40, m44, m56, m60]           __1_00
1        I1         0000000010                                 [m5, m13]                                   00_101
2        I2         0000000100                                 [m5, m37]                                   _00101
3        I3         0000001000  [m24, m25, m28, m29, m56, m57, m60, m61]          _11_0_
4        I4         0000010000                                [m23, m55]                                  _10111
5        I5         0000100000                                  [m5, m7]                                   0001_1
6        I6         0001000000                      [m40, m42, m44, m46]                         101__0
7        I7         0010000000                                 [m7, m23]                                  0_0111
8        I8         0100000000    [m8, m9, m12, m13, m24, m25, m28, m29]           0_1_0_
9        I9         1000000000                                  [m0, m8]                                   00_000


Dict_1 is a dictionary whose keys corresponds to the minterm and values in that
key corresponds to the implicant which contains those minterm.
Dict_1 is:
 {'m0': ['0000000100'], 'm5': ['0000000001', '0000010000', '1000000000'], 'm7': ['0000000001', '0001000000'], 'm8': ['0000000100', '0000001000', '0010000000'], 'm9': ['0010000000'], 'm12': ['0000001000', '0010000000'], 'm13': ['0000010000', '0010000000'], 'm23': ['0001000000', '0100000000'], 'm24': ['0000001000', '0000100000', '0010000000'], 'm25': ['0000100000', '0010000000'], 'm28': ['0000001000', '0000100000', '0010000000'], 'm29': ['0000100000', '0010000000'], 'm37': ['1000000000'], 'm40': ['0000000010', '0000001000'], 'm42': ['0000000010'], 'm44': ['0000000010', '0000001000'], 'm46': ['0000000010'], 'm55': ['0100000000'], 'm56': ['0000001000', '0000100000'], 'm57': ['0000100000'], 'm60': ['0000001000', '0000100000'], 'm61': ['0000100000']}

final_list_old gives you the list of implicants which covers all the minterms
final_list_old is: ['1110100111', '1111100110']
df9 is a table created by final_list_old, which arranges the implicants
df9 is:
                          Group  ... num_term
0  [I9, I8, I7, I5, I2, I1, I0]  ...        7
1  [I9, I8, I7, I6, I5, I2, I1]  ...        7

[2 rows x 3 columns]

Your expression 1 is:
['I9', 'I8', 'I7', 'I5', 'I2', 'I1', 'I0']
b'c'de'f + bc'def + a'ce' + bce' + a'b'd'e'f' + ab'cf' + a'b'c'df 

Your expression 2 is:
['I9', 'I8', 'I7', 'I6', 'I5', 'I2', 'I1']
b'c'de'f + bc'def + a'ce' + a'c'def + bce' + a'b'd'e'f' + ab'cf' 


