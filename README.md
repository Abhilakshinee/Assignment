# Assignment
#Tables for Seasonal Flavors
CREATE TABLE SeasonalFlavors (
    id INTEGER PRIMARY KEY,
    flavor_name TEXT NOT NULL,
    season TEXT NOT NULL
);
#Tables for Ingredient Inventory
CREATE TABLE Ingredients (
    id INTEGER PRIMARY KEY,
    ingredient_name TEXT NOT NULL,
    stock INTEGER NOT NULL
);
#Tables for Customer Suggestions and Allergy Concerns
CREATE TABLE CustomerSuggestions (
    id INTEGER PRIMARY KEY,
    customer_name TEXT,
    flavor_suggestion TEXT,
    allergy_concern TEXT
);
#Establishing a Connection with SQLite
import sqlite3
def connect_db():
    return sqlite3.connect('ice_cream_parlor.db')
conn = connect_db()
#Testing the Connection
if conn:
    print("Connection successful!")
else:
    print("Connection failed!")
#Adding New Seasonal Flavors
def add_seasonal_flavor(flavor_name, season):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("INSERT INTO SeasonalFlavors (flavor_name, season) VALUES (?, ?)", (flavor_name, season))
    conn.commit()
    conn.close()
#Updating and Deleting Flavors
def update_flavor(flavor_id, new_name, new_season):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("UPDATE SeasonalFlavors SET flavor_name = ?, season = ? WHERE id = ?", (new_name, new_season, flavor_id))
    conn.commit()
    conn.close()

def delete_flavor(flavor_id):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("DELETE FROM SeasonalFlavors WHERE id = ?", (flavor_id,))
    conn.commit()
    conn.close()
#Viewing Available Seasonal Flavors
def view_seasonal_flavors():
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM SeasonalFlavors")
    flavors = cursor.fetchall()
    conn.close()
    return flavors
#Adding Ingredients
def add_ingredient(ingredient_name, stock):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("INSERT INTO Ingredients (ingredient_name, stock) VALUES (?, ?)", (ingredient_name, stock))
    conn.commit()
    conn.close()
#Updating Ingredient Stock
def update_ingredient_stock(ingredient_id, new_stock):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("UPDATE Ingredients SET stock = ? WHERE id = ?", (new_stock, ingredient_id))
    conn.commit()
    conn.close()
#Removing Ingredients
def delete_ingredient(ingredient_id):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("DELETE FROM Ingredients WHERE id = ?", (ingredient_id,))
    conn.commit()
    conn.close()
#Viewing Ingredient Inventory
def view_ingredients():
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM Ingredients")
    ingredients = cursor.fetchall()
    conn.close()
    return ingredients
#Adding New Flavor Suggestions
def add_suggestion(customer_name, flavor_suggestion, allergy_concern):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("INSERT INTO CustomerSuggestions (customer_name, flavor_suggestion, allergy_concern) VALUES (?, ?, ?)", (customer_name, flavor_suggestion, allergy_concern))
    conn.commit()
    conn.close()
#Viewing and Managing Suggestions
def view_suggestions():
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM CustomerSuggestions")
    suggestions = cursor.fetchall()
    conn.close()
    return suggestions
#Adding Allergens to the Database
def add_allergen(allergen_name):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("INSERT INTO Allergens (allergen_name) VALUES (?)", (allergen_name,))
    conn.commit()
    conn.close()
#Viewing Existing Allergens
def view_allergens():
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM Allergens")
    allergens = cursor.fetchall()
    conn.close()
    return allergens
#Updating Allergen Information
def update_allergen(allergen_id, new_name):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("UPDATE Allergens SET allergen_name = ? WHERE id = ?", (new_name, allergen_id))
    conn.commit()
    conn.close()
#Maintaining a Cart of Favorite Products
cart = []

def add_to_cart(product_id):
    cart.append(product_id)

def view_cart():
    return cart

def remove_from_cart(product_id):
    cart.remove(product_id)
#Searching and Filtering Offerings
def search_flavors(search_term):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM SeasonalFlavors WHERE flavor_name LIKE ?", ('%' + search_term + '%',))
    results = cursor.fetchall()
    conn.close()
    return results

def filter_by_season(season):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM SeasonalFlavors WHERE season = ?", (season,))
    results = cursor.fetchall()
    conn.close()
    return results
#Adding Allergens if They Don’t Already Exist
def add_unique_allergen(allergen_name):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM Allergens WHERE allergen_name = ?", (allergen_name,))
    existing = cursor.fetchone()
    if not existing:
        cursor.execute("INSERT INTO Allergens (allergen_name) VALUES (?)", (allergen_name,))
        conn.commit()
    conn.close()
#Creating the User Interface
def main_menu():
    while True:
        print("Welcome to the Ice Cream Parlor!")
        print("1. Manage Seasonal Flavors")
        print("2. Manage Ingredients")
        print("3. Handle Customer Suggestions")
        print("4. Manage Allergens")
        print("5. View Cart")
        print("6. Exit")
        
        choice = input("Choose an option: ")
        
        if choice == '1':
            manage_seasonal_flavors()
        elif choice == '2':
            manage_ingredients()
        elif choice == '3':
            handle_customer_suggestions()
        elif choice == '4':
            manage_allergens()
        elif choice == '5':
            print(view_cart())
        elif choice == '6':
            break
        else:
            print("Invalid option. Please try again.")

def manage_seasonal_flavors():
    # Implementation goes here

def manage_ingredients():
    # Implementation goes here

def handle_customer_suggestions():
    # Implementation goes here

def manage_allergens():
    # Implementation goes here

if __name__ == "__main__":
    main_menu()
#Adding Items to the Cart
def add_to_cart(product_id):
    cart.append(product_id)
    print(f"Product {product_id} added to cart.")
#Viewing cart items
def view_cart():
    return cart
#Removing items from cart
def remove_from_cart(product_id):
    cart.remove(product_id)
    print(f"Product {product_id} removed from cart.")
#Implementing Search by Flavor Name
def search_flavors(search_term):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM SeasonalFlavors WHERE flavor_name LIKE ?", ('%' + search_term + '%',))
    results = cursor.fetchall()
    conn.close()
    return results
#Filtering by Seasonal Offerings and Ingredients
def filter_by_season(season):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM SeasonalFlavors WHERE season = ?", (season,))
    results = cursor.fetchall()
    conn.close()
    return results
#User Input for New Allergens
def add_unique_allergen(allergen_name):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM Allergens WHERE allergen_name = ?", (allergen_name,))
    existing = cursor.fetchone()
    if not existing:
        cursor.execute("INSERT INTO Allergens (allergen_name) VALUES (?)", (allergen_name,))
        conn.commit()
    conn.close()
#Checking and Updating Existing Allergens
def update_allergen(allergen_id, new_name):
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("UPDATE Allergens SET allergen_name = ? WHERE id = ?", (new_name, allergen_id))
    conn.commit()
    conn.close()

Testing the application:
import unittest

class TestIceCreamParlor(unittest.TestCase):
    
    def test_add_seasonal_flavor(self):
        add_seasonal_flavor('Mango', 'Summer')
        flavors = view_seasonal_flavors()
        self.assertIn(('Mango', 'Summer'), flavors)
    
    def test_add_ingredient(self):
        add_ingredient('Chocolate', 20)
        ingredients = view_ingredients()
        self.assertIn(('Chocolate', 20), ingredients)
    
    def test_add_suggestion(self):
        add_suggestion('John Doe', 'Vanilla Mint', 'None')
        suggestions = view_suggestions()
        self.assertIn(('John Doe', 'Vanilla Mint', 'None'), suggestions)

if __name__ == '__main__':
    unittest.main()
