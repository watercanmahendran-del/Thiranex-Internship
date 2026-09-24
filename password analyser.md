import re

# Common passwords
common_passwords = [
    "password",
    "123456",
    "12345678",
    "qwerty",
    "admin",
    "welcome",
    "password123"
]


def check_password(password):

    score = 0
    suggestions = []

    # Check length
    if len(password) >= 8:
        score += 1
    else:
        suggestions.append("Use at least 8 characters.")

    # Check uppercase
    if re.search(r"[A-Z]", password):
        score += 1
    else:
        suggestions.append("Add at least one uppercase letter.")

    # Check lowercase
    if re.search(r"[a-z]", password):
        score += 1
    else:
        suggestions.append("Add at least one lowercase letter.")

    # Check number
    if re.search(r"[0-9]", password):
        score += 1
    else:
        suggestions.append("Add at least one number.")

    # Check special character
    if re.search(r"[^A-Za-z0-9]", password):
        score += 1
    else:
        suggestions.append("Add at least one special character.")

    # Check common password
    if password.lower() not in common_passwords:
        score += 1
    else:
        suggestions.append("Avoid using common passwords.")

    # Determine strength
    if score <= 2:
        strength = "WEAK"
    elif score <= 4:
        strength = "MEDIUM"
    else:
        strength = "STRONG"

    # Display result
    print("\n--------------------------------")
    print("     PASSWORD STRENGTH RESULT")
    print("--------------------------------")

    print("Password Length :", len(password))
    print("Score           :", score, "/ 6")
    print("Strength        :", strength)

    if suggestions:
        print("\nSuggestions:")
        for suggestion in suggestions:
            print("-", suggestion)
    else:
        print("\nYour password satisfies all basic checks!")


# Main program

print("===================================")
print("     PASSWORD STRENGTH ANALYZER")
print("===================================")

password = input("Enter your password: ")

check_password(password)
