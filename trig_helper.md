# Trigonometry Helper Skill

This skill helps calculate trigonometric values and solve triangle problems interactively.

## Description
An interactive tool that calculates sine, cosine, tangent values and solves right-angled triangle problems. The helper can find missing side lengths or angles when given known values using trigonometric ratios and the Pythagorean theorem. Includes Python code that can be run to compute solutions when the user inputs their triangle measurements.

## Usage
```
/trig-helper
```

## Implementation
```python
import math

def calculate_trig_values(angle_degrees):
    """Calculate sine, cosine, and tangent for a given angle in degrees"""
    angle_radians = math.radians(angle_degrees)

    sin_val = math.sin(angle_radians)
    cos_val = math.cos(angle_radians)
    tan_val = math.tan(angle_radians)

    return sin_val, cos_val, tan_val

def solve_right_triangle_sides_and_angles():
    """Interactive function to solve right-angled triangle problems"""
    print("Right Triangle Solver")
    print("====================")
    print("Given different combinations of sides and angles, I can find missing values.")
    print("Note: Angle C is always 90° in a right triangle (angle opposite the hypotenuse).")
    print("")

    print("What information do you have?")
    print("1. Two sides (for example, legs a and b)")
    print("2. One side and one acute angle (for example, side a and angle A)")
    print("3. Hypotenuse and one leg")
    print("4. Just an angle - find trigonometric ratios")

    choice = input("Enter choice (1-4): ")

    if choice == "1":
        print("\nSolving with two known sides...")
        a = float(input("Enter length of side a (adjacent to angle A): "))
        b = float(input("Enter length of side b (opposite to angle A): "))

        # Calculate hypotenuse using Pythagorean theorem
        c = math.sqrt(a**2 + b**2)

        # Calculate angles
        angle_A_rad = math.atan(a / b)  # angle opposite to side a
        angle_B_rad = math.atan(b / a)  # angle opposite to side b

        angle_A_deg = math.degrees(angle_A_rad)
        angle_B_deg = math.degrees(angle_B_rad)

        print(f"\nResults:")
        print(f"Hypotenuse (side c): {c:.4f}")
        print(f"Angle A: {angle_A_deg:.4f}°")
        print(f"Angle B: {angle_B_deg:.4f}°")
        print(f"Angle C: 90.0000°")

    elif choice == "2":
        print("\nSolving with one side and one acute angle...")
        side_choice = input("Which side do you know? (a, b, or c): ").lower()
        known_side = float(input(f"Enter length of side {side_choice}: "))
        angle_choice = input("Which angle do you know? (A or B): ").upper()
        known_angle = float(input(f"Enter angle {angle_choice} in degrees: "))

        known_angle_rad = math.radians(known_angle)

        if side_choice == "a" and angle_choice == "A":
            # Find side b using tan(A) = a/b, so b = a/tan(A)
            b = a / math.tan(known_angle_rad)
            # Find hypotenuse using sin(A) = a/c, so c = a/sin(A)
            c = a / math.sin(known_angle_rad)
            # Calculate angle B = 90 - A
            angle_B = 90 - known_angle

        elif side_choice == "a" and angle_choice == "B":
            # Find side b using tan(B) = b/a, so b = a*tan(B)
            b = known_side * math.tan(known_angle_rad)
            # Find hypotenuse using cos(B) = a/c, so c = a/cos(B)
            c = known_side / math.cos(known_angle_rad)
            # Calculate angle A = 90 - B
            angle_A = 90 - known_angle

        elif side_choice == "b" and angle_choice == "A":
            # Find side a using tan(A) = a/b, so a = b*tan(A)
            a = known_side * math.tan(known_angle_rad)
            # Find hypotenuse using cos(A) = b/c, so c = b/cos(A)
            c = known_side / math.cos(known_angle_rad)
            # Calculate angle B = 90 - A
            angle_B = 90 - known_angle

        elif side_choice == "b" and angle_choice == "B":
            # Find side a using tan(B) = b/a, so a = b/tan(B)
            a = known_side / math.tan(known_angle_rad)
            # Find hypotenuse using sin(B) = b/c, so c = b/sin(B)
            c = known_side / math.sin(known_angle_rad)
            # Calculate angle A = 90 - B
            angle_A = 90 - known_angle

        elif side_choice == "c" and angle_choice == "A":
            # Find side a using sin(A) = a/c, so a = c*sin(A)
            a = known_side * math.sin(known_angle_rad)
            # Find side b using cos(A) = b/c, so b = c*cos(A)
            b = known_side * math.cos(known_angle_rad)
            # Calculate angle B = 90 - A
            angle_B = 90 - known_angle

        elif side_choice == "c" and angle_choice == "B":
            # Find side b using sin(B) = b/c, so b = c*sin(B)
            b = known_side * math.sin(known_angle_rad)
            # Find side a using cos(B) = a/c, so a = c*cos(B)
            a = known_side * math.cos(known_angle_rad)
            # Calculate angle A = 90 - B
            angle_A = 90 - known_angle
        else:
            print("Invalid combination entered!")
            return

        # Print results
        print(f"\nResults:")
        print(f"Side a: {a:.4f}")
        print(f"Side b: {b:.4f}")
        print(f"Side c (hypotenuse): {c:.4f}")

        if 'angle_A' in locals():
            print(f"Angle A: {angle_A:.4f}°")
        if 'angle_B' in locals():
            print(f"Angle B: {angle_B:.4f}°")

        print(f"Angle C: 90.0000°")

    elif choice == "3":
        print("\nSolving with hypotenuse and one leg...")
        c = float(input("Enter length of hypotenuse (side c): "))
        known_leg = input("Which leg do you know? (a or b): ").lower()
        known_length = float(input(f"Enter length of side {known_leg}: "))

        if known_leg == "a":
            # Calculate unknown leg using Pythagorean theorem
            b = math.sqrt(c**2 - known_length**2)
            # Calculate angles
            angle_A_rad = math.asin(known_length / c)  # sin(A) = a/c
            angle_A_deg = math.degrees(angle_A_rad)
            angle_B_deg = 90 - angle_A_deg
        else:  # known_leg == "b"
            # Calculate unknown leg using Pythagorean theorem
            a = math.sqrt(c**2 - known_length**2)
            # Calculate angles
            angle_B_rad = math.asin(known_length / c)  # sin(B) = b/c
            angle_B_deg = math.degrees(angle_B_rad)
            angle_A_deg = 90 - angle_B_deg

        # Print results
        print(f"\nResults:")
        if known_leg == "a":
            print(f"Side a: {known_length:.4f}")
            print(f"Side b: {b:.4f}")
        else:
            print(f"Side a: {a:.4f}")
            print(f"Side b: {known_length:.4f}")

        print(f"Side c (hypotenuse): {c:.4f}")
        print(f"Angle A: {angle_A_deg:.4f}°")
        print(f"Angle B: {angle_B_deg:.4f}°")
        print(f"Angle C: 90.0000°")

    elif choice == "4":
        print("\nCalculating trigonometric ratios for a given angle...")
        angle = float(input("Enter the angle in degrees: "))

        sin_val, cos_val, tan_val = calculate_trig_values(angle)

        print(f"\nTrigonometric Values for {angle}°:")
        print(f"sin({angle}°) = {sin_val:.6f}")
        print(f"cos({angle}°) = {cos_val:.6f}")
        print(f"tan({angle}°) = {tan_val:.6f}")

        # Additional reciprocal functions
        print(f"csc({angle}°) = {1/sin_val:.6f} (cosecant)")
        print(f"sec({angle}°) = {1/cos_val:.6f} (secant)")
        print(f"cot({angle}°) = {1/tan_val:.6f} (cotangent)")

    else:
        print("Invalid choice!")

def main():
    print("Trigonometry Helper")
    print("===================")
    print("This tool helps calculate trigonometric values and solve triangle problems.")
    print("")

    solve_right_triangle_sides_and_angles()

if __name__ == "__main__":
    main()
```

## Tags
- mathematics
- trigonometry
- geometry
- calculator
- education
- problem-solving