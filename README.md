# lab4

this is the policy

package lab4work;

public abstract class Policy {
    protected String firstName, lastName;

    public Policy(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    // Abstract method to be implemented by subclasses
    public abstract double computeCommission();

    // Common method for printing policy headers
    public void printPolicyHeader(String policyType) {
        System.out.println("\n" + policyType + " Policy");
        System.out.println("-----------");
        System.out.println("Name: " + firstName + " " + lastName);
    }

    // Abstract method for providing policy details
    public abstract String toString();
}


this is the auto

public class Auto extends Policy {
    private String make, model;
    private double liability, collision;

    public Auto(String firstName, String lastName, String make, String model, double liability, double collision) {
        super(firstName, lastName);
        this.make = make;
        this.model = model;
        this.liability = liability;
        this.collision = collision;
    }

    @Override
    public double computeCommission() {
        return (liability + collision) * 0.3; // 30% commission
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("Make: ").append(make).append("\n");
        sb.append("Model: ").append(model).append("\n");
        sb.append(String.format("Liability: $%,.2f%n", liability));
        sb.append(String.format("Collision: $%,.2f%n", collision));
        sb.append(String.format("Commission: $%,.2f%n", computeCommission()));
        return sb.toString();
    }
}


this is the home

package lab4work;

public class Home extends Policy {
    private int squareFootage;
    private double dwelling, contents, liability;

    public Home(String firstName, String lastName, int squareFootage, double dwelling, double contents, double liability) {
        super(firstName, lastName);
        this.squareFootage = squareFootage;
        this.dwelling = dwelling;
        this.contents = contents;
        this.liability = liability;
    }

    @Override
    public double computeCommission() {
        return (dwelling + contents + liability) * 0.2; // 20% commission
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("Square Footage: ").append(squareFootage).append("\n");
        sb.append(String.format("Dwelling: $%,.2f%n", dwelling));
        sb.append(String.format("Contents: $%,.2f%n", contents));
        sb.append(String.format("Liability: $%,.2f%n", liability));
        sb.append(String.format("Commission: $%,.2f%n", computeCommission()));
        return sb.toString();
    }
}


this is the life

package lab4work;

public class Life extends Policy {
    private int age;
    private double term;

    public Life(String firstName, String lastName, int age, double term) {
        super(firstName, lastName);
        this.age = age;
        this.term = term;
    }

    @Override
    public double computeCommission() {
        return term * 0.2; // 20% commission
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("Age: ").append(age).append("\n");
        sb.append(String.format("Term: $%,.2f%n", term));
        sb.append(String.format("Commission: $%,.2f%n", computeCommission()));
        return sb.toString();
    }
}


this is the claculator

package lab4work;

import java.util.ArrayList;

public class Calculator {
    // Method to display the commission for all policies
    public static void displayCommission(ArrayList<Policy> policies) {
        // List all policies
        for (Policy policy : policies) {
            // Compute commission
            policy.computeCommission();
            // Print the policy
            System.out.println(policy);
        }
    }
}



this is the driver

package lab4work;

import java.util.ArrayList;
import java.util.Scanner;

public class Driver {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        ArrayList<Policy> policies = new ArrayList<>();
        boolean exit = false;

        while (!exit) {
            System.out.println("\nWelcome to Parkland Insurance\n");
            System.out.println("Enter any of the following:");
            System.out.println("1) Enter auto insurance policy information");
            System.out.println("2) Enter home insurance policy information");
            System.out.println("3) Enter life insurance policy information");
            System.out.println("4) Print all sales entered");
            System.out.println("5) Quit");
            System.out.print("Choose an option: ");
            int choice = input.nextInt();
            input.nextLine(); // Consume the newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter first name: ");
                    String firstName = input.nextLine();
                    System.out.print("Enter last name: ");
                    String lastName = input.nextLine();
                    System.out.print("Enter make: ");
                    String make = input.nextLine();
                    System.out.print("Enter model: ");
                    String model = input.nextLine();
                    System.out.print("Enter liability amount: ");
                    double liability = input.nextDouble();
                    System.out.print("Enter collision amount: ");
                    double collision = input.nextDouble();
                    input.nextLine(); // Consume newline
                    policies.add(new Auto(firstName, lastName, make, model, liability, collision));
                    break;

                case 2:
                    System.out.print("Enter first name: ");
                    firstName = input.nextLine();
                    System.out.print("Enter last name: ");
                    lastName = input.nextLine();
                    System.out.print("Enter square footage: ");
                    int squareFootage = input.nextInt();
                    System.out.print("Enter dwelling amount: ");
                    double dwelling = input.nextDouble();
                    System.out.print("Enter contents amount: ");
                    double contents = input.nextDouble();
                    System.out.print("Enter liability amount: ");
                    liability = input.nextDouble();
                    input.nextLine(); // Consume newline
                    policies.add(new Home(firstName, lastName, squareFootage, dwelling, contents, liability));
                    break;

                case 3:
                    System.out.print("Enter first name: ");
                    firstName = input.nextLine();
                    System.out.print("Enter last name: ");
                    lastName = input.nextLine();
                    System.out.print("Enter age: ");
                    int age = input.nextInt();
                    System.out.print("Enter term amount: ");
                    double term = input.nextDouble();
                    input.nextLine(); // Consume newline
                    policies.add(new Life(firstName, lastName, age, term));
                    break;

                case 4:
                    Calculator.displayCommission(policies);
                    break;

                case 5:
                    exit = true;
                    System.out.println("Goodbye!");
                    break;

                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }

        input.close();
    }
}
