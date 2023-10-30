# PERSONAL-HEALTH-ASSISTANT_JAVA
//"Online Personal Training Assistant" project emerges as a powerful tool bridging the gap between fitness goals and expert guidance
//JAVA PROGRAM
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class OnlinePersonalTrainingAssistant {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            UserInterface ui = new UserInterface();
            ui.authenticateUser();
        });
    }
}

class User {
    private String name;
    private int age;
    private double weight;
    private double height; // Height in centimeters
    private double bmi;

    public User(String name, int age, double weight, double height, double bmi) {
        this.name = name;
        this.age = age;
        this.weight = weight;
        this.height = height;
        this.bmi = bmi;
    }

    public String getName() {
        return name;
    }

    public String getAge() {
        return Integer.toString(age);
    }

    public String getWeight() {
        return Double.toString(weight);
    }

    public String getHeight() {
        return Double.toString(height);
    }

    public String getBMI() {
        return String.format("%.2f", bmi);
    }

    public String getWorkoutAndDiet() {
        String workoutPlan = "Your personalized workout plan:\n" +
            "Monday: Chest and Triceps\n" +
            "Tuesday: Back and Biceps\n" +
            "Wednesday: Rest day\n" +
            "Thursday: Legs and Shoulders\n" +
            "Friday: Cardio and Abs\n" +
            "Saturday: Rest day\n" +
            "Sunday: Rest day";

        String dietChart = "Your personalized diet chart:\n" +
            "Breakfast: Oatmeal with fruits and a glass of milk\n" +
            "Mid-Morning Snack: Greek yogurt with honey\n" +
            "Lunch: Grilled chicken breast with brown rice and vegetables\n" +
            "Afternoon Snack: Mixed nuts and a banana\n" +
            "Dinner: Baked salmon with quinoa and steamed broccoli\n" +
            "Before Bed: A glass of warm milk";

        return workoutPlan + "\n\n" + dietChart;
    }

    // Add a method to interpret the BMI value
    public String getBMIInterpretation() {
        double bmiValue = this.bmi;
        String interpretation;

        if (bmiValue < 18.5) {
            interpretation = "You are underweight.";
        } else if (bmiValue >= 18.5 && bmiValue < 24.9) {
            interpretation = "You are in the healthy weight range.";
        } else if (bmiValue >= 25 && bmiValue < 29.9) {
            interpretation = "You are overweight.";
        } else {
            interpretation = "You are obese.";
        }

        return interpretation;
    }
}

class UserInterface {
    private User currentUser;

    public void authenticateUser() {
        // Get user input
        String name = JOptionPane.showInputDialog(null, "Enter your name:");
        int age = Integer.parseInt(JOptionPane.showInputDialog(null, "Enter your age:"));
        double weight = Double.parseDouble(JOptionPane.showInputDialog(null, "Enter your weight (in kg):"));
        double heightCm = Double.parseDouble(JOptionPane.showInputDialog(null, "Enter your height (in cm):")); // Height in cm

        // Convert height to meters
        double heightM = heightCm / 100.0;

        // Calculate BMI
        double bmi = weight / (heightM * heightM);

        currentUser = new User(name, age, weight, heightCm, bmi); // Store height in cm

        displayGUI();
    }

    private void displayGUI() {
        JFrame frame = new JFrame("Online Personal Training Assistant");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 300);

        JTextArea outputTextArea = new JTextArea();
        outputTextArea.setEditable(false);

        JScrollPane scrollPane = new JScrollPane(outputTextArea);
        frame.add(scrollPane);

        String name = currentUser.getName();
        String age = currentUser.getAge();
        String weight = currentUser.getWeight();
        String height = currentUser.getHeight();
        String bmiMessage = "Hello " + name + ", your BMI is " + currentUser.getBMI();

        // Get BMI interpretation
        String bmiInterpretation = currentUser.getBMIInterpretation();

        String workoutAndDiet = currentUser.getWorkoutAndDiet();

        outputTextArea.append("Name: " + name + "\nAge: " + age + " years\nWeight: " + weight + " kg\nHeight: " + height + " cm\n");
        outputTextArea.append(bmiMessage + "\n" + bmiInterpretation + "\n\n" + workoutAndDiet);

        frame.setVisible(true);
    }
}

