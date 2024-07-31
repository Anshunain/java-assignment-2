package org.java.introduction;


import java.util.InputMismatchException;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Inventory inventory = new Inventory();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. Add Item");
            System.out.println("2. Update Item");
            System.out.println("3. Display Inventory");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");

            try {
                int choice = scanner.nextInt();

                switch (choice) {
                    case 1:
                        addItem(inventory, scanner);
                        break;
                    case 2:
                        updateItem(inventory, scanner);
                        break;
                    case 3:
                        inventory.displayInventory();
                        break;
                    case 4:
                        System.out.println("Exiting...");
                        return;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                        break;
                }
            } catch (InputMismatchException e) {
                ExceptionHandling.handleInputMismatchException(e);
                scanner.next(); // clear the invalid input
            } catch (Exception e) {
                ExceptionHandling.handleException(e);
            }
        }
    }

    private static void addItem(Inventory inventory, Scanner scanner) {
        System.out.print("Enter name: ");
        String name = scanner.next();
        System.out.print("Enter quantity: ");
        int quantity = scanner.nextInt();
        System.out.print("Enter price: ");
        double price = scanner.nextDouble();

        if (InputValidator.validateQuantity(quantity) && InputValidator.validatePrice(price)) {
            inventory.addItem(new Item(name, quantity, price));
        } else {
            System.out.println("Invalid input values for quantity or price.");
        }
    }

    private static void updateItem(Inventory inventory, Scanner scanner) {
        System.out.print("Enter name of the item to update: ");
        String name = scanner.next();
        System.out.print("Enter new quantity: ");
        int quantity = scanner.nextInt();
        System.out.print("Enter new price: ");
        double price = scanner.nextDouble();

        if (InputValidator.validateQuantity(quantity) && InputValidator.validatePrice(price)) {
            inventory.updateItem(name, quantity, price);
        } else {
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
