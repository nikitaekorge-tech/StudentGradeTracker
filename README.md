# StudentGradeTracker.java

import java.util.ArrayList;
import java.util.Scanner;

// Class to store student information
class Student {
    String name;
    double grade;

    public Student(String name, double grade) {
        this.name = name;
        this.grade = grade;
    }
}

public class StudentGradeTracker {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<Student> studentList = new ArrayList<>();

        System.out.println("=== Student Grade Tracker ===");
        
        // 1. Taking input from the user
        while (true) {
            System.out.print("\nEnter student name (or type 'exit' to stop): ");
            String name = scanner.nextLine();
            
            if (name.equalsIgnoreCase("exit")) {
                break;
            }

            System.out.print("Enter grade for " + name + ": ");
            double grade;
            try {
                grade = Double.parseDouble(scanner.nextLine());
                if (grade < 0 || grade > 100) {
                    System.out.println("Invalid input. Please enter a grade between 0 and 100.");
                    continue;
                }
            } catch (NumberFormatException e) {
                System.out.println("Error: Please enter a valid numerical grade.");
                continue;
            }

            // Adding student to the list
            studentList.add(new Student(name, grade));
        }

        // Stop the program if no data was entered
        if (studentList.isEmpty()) {
            System.out.println("\nNo data entered. Exiting program.");
            scanner.close();
            return;
        }

        // 2. Performing calculations
        double total = 0;
        double highest = studentList.get(0).grade;
        double lowest = studentList.get(0).grade;
        String highestStudent = studentList.get(0).name;
        String lowestStudent = studentList.get(0).name;

        for (Student s : studentList) {
            total += s.grade;

            // Checking for highest grade
            if (s.grade > highest) {
                highest = s.grade;
                highestStudent = s.name;
            }

            // Checking for lowest grade
            if (s.grade < lowest) {
                lowest = s.grade;
                lowestStudent = s.name;
            }
        }

        double average = total / studentList.size();

        // 3. Displaying the Summary Report
        System.out.println("\n=================================");
        System.out.println("         SUMMARY REPORT          ");
        System.out.println("=================================");
        System.out.println(String.format("%-15s | %-10s", "Student Name", "Grade"));
        System.out.println("---------------------------------");
        for (Student s : studentList) {
            System.out.println(String.format("%-15s | %-10.2f", s.name, s.grade));
        }
        System.out.println("---------------------------------");
        
        // Final Results
        System.out.println("Total Students  : " + studentList.size());
        System.out.printf("Average Grade   : %.2f\n", average);
        System.out.printf("Highest Grade   : %.2f (%s)\n", highest, highestStudent);
        System.out.printf("Lowest Grade    : %.2f (%s)\n", lowest, lowestStudent);
        System.out.println("=================================");

        scanner.close();
    }
}



##output:-



```text
=== Student Grade Tracker ===

Enter student name (or type 'exit' to stop): Rahul
Enter grade for Rahul: 85.5

Enter student name (or type 'exit' to stop): Priya
Enter grade for Priya: 92.0

Enter student name (or type 'exit' to stop): Amit
Enter grade for Amit: 78.0

Enter student name (or type 'exit' to stop): exit

=================================
         SUMMARY REPORT          
=================================
Student Name    | Grade     
---------------------------------
Rahul           | 85.50     
Priya           | 92.00     
Amit            | 78.00     
---------------------------------
Total Students  : 3
Average Grade   : 85.17
Highest Grade   : 92.00 (Priya)
Lowest Grade    : 78.00 (Amit)
=================================
```
