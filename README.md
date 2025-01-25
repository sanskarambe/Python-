#python
import random
import string

# Predefined lists of adjectives and nouns
adjectives = ["Happy", "Cool", "Fierce", "Clever", "Quick"]
nouns = ["Tiger", "Dragon", "Phoenix", "Panda", "Wolf"]

def generate_username(include_numbers=True, include_specials=False, username_length=None):
    # Choose random adjective and noun
    adjective = random.choice(adjectives)
    noun = random.choice(nouns)
    username = adjective + noun
    
    # Add numbers if specified
    if include_numbers:
        username += str(random.randint(0, 999))
    
    # Add special characters if specified
    if include_specials:
        username += random.choice(string.punctuation)
    
    # Adjust length if specified
    if username_length:
        username = username[:username_length]
    
    return username

def save_usernames_to_file(usernames, filename="usernames.txt"):
    with open(filename, "w") as file:
        file.write("\n".join(usernames))
    print(f"Usernames saved to {filename}.")

def main():
    print("Welcome to the Random Username Generator!")
    include_numbers = input("Include numbers? (yes/no): ").strip().lower() == "yes"
    include_specials = input("Include special characters? (yes/no): ").strip().lower() == "yes"
    username_length = input("Specify username length (or press Enter to skip): ").strip()
    username_length = int(username_length) if username_length.isdigit() else None

    num_usernames = int(input("How many usernames would you like to generate? "))
    usernames = [
        generate_username(include_numbers, include_specials, username_length)
        for _ in range(num_usernames)
    ]
    
    print("\nGenerated Usernames:")
    print("\n".join(usernames))
    
    save_option = input("\nSave these usernames to a file? (yes/no): ").strip().lower()
    if save_option == "yes":
        save_usernames_to_file(usernames)

if __name__ == "__main__":
    main()
