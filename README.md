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
