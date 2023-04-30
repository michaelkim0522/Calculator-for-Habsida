# Calculator-for-Habsida
First version of my calculator, unable to perform operations in the correct arithmetic order
import java.util.Scanner;

public class Calculator1 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
         System.out.println("Enter an arithmetic operation:");

        try {
            String expression = input.nextLine();
            String[] tokens = expression.split(" ");

            if (tokens.length == 3) {
                int a = Integer.parseInt(tokens[0]);
                int b = Integer.parseInt(tokens[2]);
                char op = tokens[1].charAt(0);

                int result;
                switch (op) {
                    case '+':
                        result = a + b;
                        break;
                    case '-':
                        result = a - b;
                        break;
                    case '*':
                        result = a * b;
                        break;
                    case '/':
                        result = a / b;
                        break;
                    default:
                        throw new IllegalArgumentException("Invalid operator: " + op);
                }

                System.out.println(result);
            } else if (tokens.length == 5) {
                int a = Integer.parseInt(tokens[0]);
                int b = Integer.parseInt(tokens[2]);
                int c = Integer.parseInt(tokens[4]);
                char op1 = tokens[1].charAt(0);
                char op2 = tokens[3].charAt(0);

                int result1, result2;
                switch (op1) {
                    case '+':
                        result1 = a + b;
                        break;
                    case '-':
                        result1 = a - b;
                        break;
                    case '*':
                        result1 = a * b;
                        break;
                    case '/':
                        result1 = a / b;
                        break;
                    default:
                        throw new IllegalArgumentException("Invalid operator: " + op1);
                }

                switch (op2) {
                    case '+':
                        result2 = result1 + c;
                        break;
                    case '-':
                        result2 = result1 - c;
                        break;
                    case '*':
                        result2 = result1 * c;
                        break;
                    case '/':
                        result2 = result1 / c;
                        break;
                    default:
                        throw new IllegalArgumentException("Invalid operator: " + op2);
                }

                System.out.println(result2);
            } else {
                throw new IllegalArgumentException("Invalid expression: " + expression);
            }
        } catch (Exception e) {
            System.err.println(e.getMessage());
            System.exit(1);
        } finally {
            input.close();
        }
    }
}

Final version of my Java calculator for Habsida school
import java.util.Scanner;

public class Calculator2 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("Enter an arithmetic operation:");

        try {
            String expression = input.nextLine();
            int result = evaluateExpression(expression);
            System.out.println(result);
        } catch (Exception e) {
            System.err.println(e.getMessage());
            System.exit(1);
        } finally {
            input.close();
        }
    }

    private static int evaluateExpression(String expression) {
        String[] tokens = expression.split(" ");

        if (tokens.length == 3) {
            int a = parseIntInRange(tokens[0], -10, 10);
            int b = parseIntInRange(tokens[2], -10, 10);
            char op = tokens[1].charAt(0);
            return evaluateOperation(a, op, b);
        } else if (tokens.length == 5) {
            int a = parseIntInRange(tokens[0], -10, 10);
            char op1 = tokens[1].charAt(0);
            int b = parseIntInRange(tokens[2], -10, 10);
            char op2 = tokens[3].charAt(0);
            int c = parseIntInRange(tokens[4], -10, 10);

            if ((op1 == '*' || op1 == '/') && (op2 == '+' || op2 == '-')) {
                // Evaluate multiplication/division first, then addition/subtraction
                int ab = evaluateOperation(a, op1, b);
                return evaluateOperation(ab, op2, c);
            } else {
                // Evaluate addition/subtraction first, then multiplication/division
                int bc = evaluateOperation(b, op2, c);
                return evaluateOperation(a, op1, bc);
            }
        } else {
            throw new IllegalArgumentException("Invalid expression: " + expression);
        }
    }

    private static int evaluateOperation(int a, char op, int b) {
        switch (op) {
            case '+':
                return a + b;
            case '-':
                return a - b;
            case '*':
                return a * b;
            case '/':
                if (b == 0) {
                    throw new IllegalArgumentException("Division by zero");
                }
                return a / b;
            default:
                throw new IllegalArgumentException("Invalid operator: " + op);
        }
    }

    private static int parseIntInRange(String str, int min, int max) {
        int value = Integer.parseInt(str);
        if (value < min || value > max) {
            throw new IllegalArgumentException("Value out of range: " + value);
        }
        return value;
    }
}
