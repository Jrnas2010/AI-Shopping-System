import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Animal class representing a generic animal
class Animal {
    private String name;
    private String species;
    private String habitat;

    public Animal(String name, String species, String habitat) {
        this.name = name;
        this.species = species;
        this.habitat = habitat;
    }

    public String getName() {
        return name;
    }

    public String getSpecies() {
        return species;
    }

    public String getHabitat() {
        return habitat;
    }

    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Species: " + species);
        System.out.println("Habitat: " + habitat);
    }
}

// Zoo class to manage animals
class Zoo {
    private List<Animal> animals;

    public Zoo() {
        animals = new ArrayList<>();
    }

    public void addAnimal(Animal animal) {
        animals.add(animal);
        System.out.println("Animal added successfully!");
    }

    public void listAnimals() {
        if (animals.isEmpty()) {
            System.out.println("No animals in the zoo.");
        } else {
            System.out.println("Animals in the zoo:");
            for (Animal animal : animals) {
                animal.displayInfo();
                System.out.println("--------------------");
            }
        }
    }

    public void searchAnimal(String name) {
        boolean found = false;
        for (Animal animal : animals) {
            if (animal.getName().equalsIgnoreCase(name)) {
                System.out.println("Animal found:");
                animal.displayInfo();
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Animal not found.");
        }
    }
}

// Main class to run the Zoo Management System
public class ZooManagementSystem {
    public static void main(String[] args) {
        Zoo zoo = new Zoo();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nZoo Management System");
            System.out.println("1. Add Animal");
            System.out.println("2. List Animals");
            System.out.println("3. Search Animal");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter animal name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter species: ");
                    String species = scanner.nextLine();
                    System.out.print("Enter habitat: ");
                    String habitat = scanner.nextLine();
                    zoo.addAnimal(new Animal(name, species, habitat));
                    break;
                case 2:
                    zoo.listAnimals();
                    break;
                case 3:
                    System.out.print("Enter animal name to search: ");
                    String searchName = scanner.nextLine();
                    zoo.searchAnimal(searchName);
                    break;
                case 4:
                    System.out.println("Exiting system. Goodbye!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }
}
