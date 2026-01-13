# Algebra Solver Skill

This skill helps solve algebraic problems, equations, expressions, and simple algebra queries interactively.

## Description
An interactive tool that solves linear equations, quadratic equations, and simplifies algebraic expressions. Provides step-by-step solutions for various algebraic problems including linear equations, quadratic equations, and polynomial expressions. The solver includes Python code that can be run to compute solutions when the user inputs their equations.

## Usage
```
/algebra-solver
```

## Implementation
```python
import math
import re

def solve_linear_equation(equation):
    """
    Solves linear equations of the form ax + b = c
    """
    # Remove spaces
    equation = equation.replace(" ", "")

    # Split by equals
    left, right = equation.split("=")

    # Parse left side for coefficient of x and constant
    left = left.replace("-", "+-")
    if left.startswith("+"):
        left = left[1:]

    terms = [t for t in left.split("+") if t]

    coeff_x = 0
    const_left = 0

    for term in terms:
        if 'x' in term:
            coeff_str = term.replace('x', '')
            if coeff_str == '' or coeff_str == '+':
                coeff_x += 1
            elif coeff_str == '-':
                coeff_x -= 1
            else:
                coeff_x += int(coeff_str)
        else:
            const_left += int(term)

    const_right = int(right)

    # Solve: ax + b = c => ax = c - b => x = (c - b) / a
    if coeff_x == 0:
        if const_left == const_right:
            return "Infinite solutions (identity)"
        else:
            return "No solution (contradiction)"
    else:
        x = (const_right - const_left) / coeff_x
        return f"x = {x}"

def solve_quadratic_equation(a, b, c):
    """
    Solves quadratic equations of the form ax^2 + bx + c = 0
    """
    discriminant = b**2 - 4*a*c

    if discriminant > 0:
        sqrt_discriminant = math.sqrt(discriminant)
        x1 = (-b + sqrt_discriminant) / (2*a)
        x2 = (-b - sqrt_discriminant) / (2*a)
        return f"x = {x1} or x = {x2}"
    elif discriminant == 0:
        x = -b / (2*a)
        return f"x = {x} (repeated root)"
    else:
        real_part = -b / (2*a)
        imaginary_part = math.sqrt(abs(discriminant)) / (2*a)
        return f"x = {real_part} + {imaginary_part}i or x = {real_part} - {imaginary_part}i"

def simplify_expression(expression):
    """
    Simplifies basic algebraic expressions
    """
    # This is a simplified version - a full implementation would be more complex
    # For demonstration purposes, this just evaluates expressions if they can be evaluated
    try:
        # Replace ^ with ** for Python exponentiation
        expr = expression.replace("^", "**")
        result = eval(expr)
        return f"Simplified: {result}"
    except:
        return f"Could not simplify: {expression}. This function handles basic numeric expressions."

def main():
    print("Algebra Solver")
    print("==============")
    print("Choose an option:")
    print("1. Solve linear equation (e.g., 2x + 5 = 11)")
    print("2. Solve quadratic equation (e.g., x^2 + 5x + 6 = 0)")
    print("3. Simplify expression")

    choice = input("Enter choice (1, 2, or 3): ")

    if choice == "1":
        eq = input("Enter linear equation (e.g., 2x + 5 = 11): ")
        try:
            result = solve_linear_equation(eq)
            print(f"Solution: {result}")
        except Exception as e:
            print(f"Error parsing equation: {e}")

    elif choice == "2":
        print("For quadratic equation ax^2 + bx + c = 0, enter the coefficients:")
        try:
            a = float(input("Enter coefficient a: "))
            b = float(input("Enter coefficient b: "))
            c = float(input("Enter coefficient c: "))
            result = solve_quadratic_equation(a, b, c)
            print(f"Solution: {result}")
        except ValueError:
            print("Please enter valid numbers for coefficients.")
        except Exception as e:
            print(f"Error: {e}")

    elif choice == "3":
        expr = input("Enter expression to simplify: ")
        result = simplify_expression(expr)
        print(result)

    else:
        print("Invalid choice.")

if __name__ == "__main__":
    main()
```

## Tags
- mathematics
- algebra
- education
- problem-solving
- calculator