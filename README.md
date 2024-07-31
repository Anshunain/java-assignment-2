package org.java.introduction;

import java.util.InputMismatchException;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Inventory inventory = new Inventory();
        Scanner scanner = new Scanner(System.in);

        // Main loop to display the menu and process user input
        while (true) {
            // Display menu options
            System.out.println("1. Add Item");
            System.out.println("2. Update Item");
            System.out.println("3. Display Inventory");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");

            try {
                int choice = scanner.nextInt();

                // Process user's choice
                switch (choice) {
                    case 1:
                        addItem(inventory, scanner);
                        break;
                    case 2:
                        updateItem(inventory, scanner);
                        break;
                    case 3:
                        // Display all items in the inventory
                        inventory.displayInventory();
                        break;
                    case 4:
                        System.out.println("Exiting...");
                        return;
                    default:
                        // Handle invalid menu choices
                        System.out.println("Invalid choice. Please try again.");
                        break;
                }
            } catch (InputMismatchException e) {
                // Handle input mismatch exceptions (e.g., user enters a non-integer value)
                ExceptionHandling.handleInputMismatchException(e);
                scanner.next(); // Clear the invalid input
            } catch (Exception e) {
                ExceptionHandling.handleException(e);
            }
        }
    }

    /**
     * Adds a new item to the inventory.
     *
     * @param inventory The inventory object
     * @param scanner   The scanner object to read user input
     */
    private static void addItem(Inventory inventory, Scanner scanner) {
        System.out.print("Enter name: ");
        String name = scanner.next();
        System.out.print("Enter quantity: ");
        int quantity = scanner.nextInt();
        System.out.print("Enter price: ");
        double price = scanner.nextDouble();

        if (InputValidator.validateQuantity(quantity) && InputValidator.validatePrice(price)) {
            // Add the item to the inventory if inputs are valid
            inventory.addItem(new Item(name, quantity, price));
        } else {
            // Display error message for invalid input values
            System.out.println("Invalid input values for quantity or price.");
        }
    }

    /**
     * Updates an existing item in the inventorys
     * @param inventory The inventory object
     * @param scanner   The scanner object to read user input
     */
    private static void updateItem(Inventory inventory, Scanner scanner) {
        // Prompt user for item details to update
        System.out.print("Enter name of the item to update: ");
        String name = scanner.next();
        System.out.print("Enter new quantity: ");
        int quantity = scanner.nextInt();
        System.out.print("Enter new price: ");
        double price = scanner.nextDouble();

        if (InputValidator.validateQuantity(quantity) && InputValidator.validatePrice(price)) {
            // Update the item in the inventory if inputs are valid
            inventory.updateItem(name, quantity, price);
        } else {
            // Display error message for invalid input values
            System.out.println("Invalid input values for quantity or price.");
        }
    }
}
package org.java.introduction;


public class Item {
    protected String name;
    protected int quantity;
    protected double price;

    public Item(String name, int quantity, double price) {
        this.name = name;
        this.quantity = quantity;
        this.price = price;
    }

    public void displayDetails() {
        System.out.println("Name: " + name + ", Quantity: " + quantity + ", Price: " + price);
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public double getPrice() {
        return price;
    }
}
package org.java.introduction;

import java.util.ArrayList;
import java.util.NoSuchElementException;

public class Inventory {
    private ArrayList<Item> items;

    public Inventory() {
        items = new ArrayList<>();
    }

    public void addItem(Item item) {
        items.add(item);
    }

    public void updateItem(String itemName, int quantity, double price) {
        for (Item item : items) {
            if (item.getName().equals(itemName)) {
                item.setQuantity(quantity);
                item.setPrice(price);
                return;
            }
        }
        System.out.println("Item not found.");
    }

    public void displayInventory() {
        for (Item item : items) {
            item.displayDetails();
        }
    }
}
package org.java.introduction;


public class InputValidator {
    public static boolean validateQuantity(int quantity) {
        return quantity >= 0;
    }

    public static boolean validatePrice(double price) {
        return price >= 0;
    }
}
package org.java.introduction;


import java.util.InputMismatchException;
import java.util.NoSuchElementException;

public class ExceptionHandling {
    public static void handleException(Exception e) {
        System.out.println("Error: " + e.getMessage());
    }

    public static void handleInputMismatchException(InputMismatchException e) {
        System.out.println("Input Mismatch Error: " + e.getMessage());
    }

    public static void handleNoSuchElementException(NoSuchElementException e) {
        System.out.println("No Such Element Error: " + e.getMessage());
    }

    public static void handleIllegalArgumentException(IllegalArgumentException e) {
        System.out.println("Illegal Argument Error: " + e.getMessage());
    }
}
