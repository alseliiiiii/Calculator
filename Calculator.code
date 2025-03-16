import java.util.*;

public class Calculator {
    private static final Scanner s = new Scanner(System.in);
    private static final List<String> history = new ArrayList<>();

    private static int getOp(String exp, int cur) {
        Scanner s = new Scanner(exp.substring(cur));
        s.useDelimiter("[^0-9]");
        return s.nextInt();
    }

    private static double doOp(double op1, double op2, char operator) throws Exception {
        switch (operator) {
            case '+': return op1 + op2;
            case '-': return op1 - op2;
            case '*': return op1 * op2;
            case '/': 
                if (op2 == 0) throw new ArithmeticException("Division by zero");
                return op1 / op2;
            case '%': 
                if (op2 == 0) throw new ArithmeticException("Modulo by zero");
                return op1 % op2;
            default: throw new Exception("Invalid operator");
        }
    }

    private static double evaluateFunction(String func, double value) throws Exception {
        switch (func) {
            case "abs": return Math.abs(value);
            case "sqrt": 
                if (value < 0) throw new ArithmeticException("Square root of negative number");
                return Math.sqrt(value);
            case "round": return Math.round(value);
            default: throw new Exception("Unknown function: " + func);
        }
    }

    private static int comparePrecedence(char op1, char op2) {
        if ((op1 == '+' || op1 == '-') && (op2 == '*' || op2 == '/' || op2 == '%')) {
            return -1;
        } else if ((op1 == '*' || op1 == '/' || op2 == '%') && (op2 == '+' || op2 == '-')) {
            return 1;
        }
        return 0;
    }

    public static void main(String[] args) throws Exception {
        boolean continueCalculation = true;

        while (continueCalculation) {
            System.out.println("Welcome to the Calculator!");
            System.out.println("Please enter your arithmetic expression: ");
            String exp = s.nextLine();

            try {
                double result = evaluateExpression(exp);
                System.out.println("Result: " + result);
                history.add(exp + " = " + result);
            } catch (Exception e) {
                System.out.println("Error: " + e.getMessage());
            }

            System.out.print("Would you like to view the calculation history? (y/n): ");
            String viewHistory = s.nextLine().trim().toLowerCase();
            if (viewHistory.equals("y")) {
                System.out.println("Calculation History:");
                for (String entry : history) {
                    System.out.println(entry);
                }
            }

            System.out.print("Do you want to continue? (y/n): ");
            String response = s.nextLine().trim().toLowerCase();
            if (response.equals("n")) {
                continueCalculation = false;
                System.out.println("Thank you for using the Calculator!");
            }
        }
    }

    private static double evaluateExpression(String exp) throws Exception {
        Stack<Character> operators = new Stack<>();
        Stack<Double> operands = new Stack<>();
        char prev = 0;

        for (int cur = 0; cur < exp.length(); cur++) {
            char currentChar = exp.charAt(cur);

            if (Character.isLetter(currentChar)) {
                StringBuilder func = new StringBuilder();
                while (cur < exp.length() && Character.isLetter(exp.charAt(cur))) {
                    func.append(exp.charAt(cur++));
                }
                cur--;
                if (cur + 2 < exp.length() && exp.charAt(cur + 1) == '(') {
                    cur += 2;
                    int start = cur;
                    int parenCount = 1;
                    while (cur < exp.length() && parenCount > 0) {
                        if (exp.charAt(cur) == '(') parenCount++;
                        if (exp.charAt(cur) == ')') parenCount--;
                        cur++;
                    }
                    cur--;
                    double value = evaluateExpression(exp.substring(start, cur));
                    operands.push(evaluateFunction(func.toString(), value));
                } else {
                    throw new Exception("Invalid function format");
                }
                continue;
            }

            switch (currentChar) {
                case '(':
                    operators.push(currentChar);
                    break;
                case '+':
                case '-':
                    if (prev == 0 || prev == '(') {
                        operands.push(0.0);
                    }
          
                case '*':
                case '/':
                case '%':
                    while (!operators.isEmpty() && operators.peek() != '(' && comparePrecedence(operators.peek(), currentChar) >= 0) {
                        double op2 = operands.pop();
                        double result = doOp(operands.pop(), op2, operators.pop());
                        operands.push(result);
                    }
                    operators.push(currentChar);
                    break;
                case ')':
                    while (!operators.isEmpty() && operators.peek() != '(') {
                        double op2 = operands.pop();
                        operands.push(doOp(operands.pop(), op2, operators.pop()));
                    }
                    if (operators.isEmpty()) {
                        throw new Exception("Unbalanced parentheses");
                    }
                    operators.pop();
                    break;
                case ' ': case '\t':
                    break;
                default:
                    if (Character.isDigit(currentChar)) {
                        int temp = getOp(exp, cur);
                        while (cur < exp.length() && Character.isDigit(exp.charAt(cur))) {
                            cur++;
                        }
                        cur--;
                        operands.push((double) temp);
                    } else {
                        throw new Exception("Invalid character");
                    }
            }
            if (!Character.isWhitespace(currentChar)) {
                prev = currentChar;
            }
        }

        while (!operators.isEmpty()) {
            double op2 = operands.pop();
            operands.push(doOp(operands.pop(), op2, operators.pop()));
        }

        return operands.pop();
    }
}
