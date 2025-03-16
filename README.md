# Project Report                                                          
## Objective:
The objective of this project is to build a simple yet functional command-line calculator in Java that supports basic arithmetic operations and advanced mathematical functions. The project also includes a history feature that allows users to review their previous calculations.


## How it works:
The calculator evaluates arithmetic expressions input by the user, supporting basic operations such as addition, subtraction, multiplication, division, and modulo. It also handles mathematical functions like absolute value, square root, and rounding. The program uses a stack-based approach to evaluate the expressions, where operators and operands are processed one by one. The precedence of operators is managed to ensure proper order of operations. Additionally, it allows users to view the history of previous calculations, storing each result with the corresponding expression for reference.

## Algorithms and Data Structures Used:

Algorithm for Expression Evaluation:
The algorithm used to evaluate expressions is based on the Shunting Yard Algorithm, which uses stacks to manage operators and operands. The algorithm processes the expression from left to right, correctly handling parentheses and operator precedence.

Data Structures:
Stack:
A stack was used to store operators and parentheses while evaluating the expression. This allowed us to respect the order of operations and handle nested parentheses effectively.
List:
A list was used to store the history of calculations, allowing the user to view previous results.
String Builder:
A StringBuilder was used to accumulate the function name (such as abs, sqrt, etc.) during parsing.

## My experience:
This project was particularly challenging for me. I faced significant difficulties while implementing the history feature and managing the sequence of algebraic operators, especially parentheses. However, I learned a lot throughout this process. Initially, I aimed to create a console-based calculator, but I realized it would be more complex than I expected. Despite this, I plan to test this version further. During the project, I explored different ways to approach the same task and experimented with using multiple classes, which was a valuable learning experience.

## Resources Used:
- YouTube channel by Kianoosh Boroojeni
- GeeksforGeeks
- W3Schools
- Chat GPT



