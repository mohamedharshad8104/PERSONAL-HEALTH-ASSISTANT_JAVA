# PERSONAL-HEALTH-ASSISTANT_JAVA
//"Online Personal Training Assistant" project emerges as a powerful tool bridging the gap between fitness goals and expert guidance
//JAVA PROGRAM
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

class User {
    private String name;
    private double weight;
    private double height;
    private int age;

    public User(String name, double weight, double height) {
        this.name = name;
        this.weight = weight;
        this.height = height;
        this.age = 0; // Age is not used for BMI calculation
    }

    public double calculateBMI() {
        double heightInMeters = height / 100;
        return weight / (heightInMeters * heightInMeters);
    }

    public void viewWorkoutPlan() {
        String workoutPlan = "Your personalized workout plan:\n" +
                "Monday: Chest and Triceps\n" +
                "Tuesday: Back and Biceps\n" +
                "Wednesday: Rest day\n" +
                "Thursday: Legs and Shoulders\n" +
                "Friday: Cardio and Abs\n" +
                "Saturday: Rest day\n" +
                "Sunday: Rest day";
        JOptionPane.showMessageDialog(null, workoutPlan, "Workout Plan", JOptionPane.INFORMATION_MESSAGE);
    }

    public void viewDietChart() {
        String dietChart = "Your personalized diet chart:\n" +
                "Breakfast: Oatmeal with fruits and a glass of milk\n" +
                "Mid-Morning Snack: Greek yogurt with honey\n" +
                "Lunch: Grilled chicken breast with brown rice and vegetables\n" +
                "Afternoon Snack: Mixed nuts and a banana\n" +
                "Dinner: Baked salmon with quinoa and steamed broccoli\n" +
                "Before Bed: A glass of warm milk";
        JOptionPane.showMessageDialog(null, dietChart, "Diet Chart", JOptionPane.INFORMATION_MESSAGE);
    }
}

class OnlinePersonalTrainingAssistant {
    private JFrame frame;
    private UserInterface userInterface;
    private User currentUser;

    public OnlinePersonalTrainingAssistant() {
        frame = new JFrame("Personal Training Assistant");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        userInterface = new UserInterface(this);
        frame.add(userInterface);

        frame.pack();
        frame.setVisible(true);
    }

    public void authenticateUser(String name, double weight, double height) {
        currentUser = new User(name, weight, height);
        currentUser.calculateBMI();
        showMainOptions();
    }

    public void showMainOptions() {
        int choice = JOptionPane.showConfirmDialog(null,
                "Choose an option:\nView Workout Plan\nView Diet Chart\nView BMI\n\nYour BMI: " + String.format("%.2f", currentUser.calculateBMI()),
                "Main Menu", JOptionPane.YES_NO_OPTION);

        if (choice == JOptionPane.YES_OPTION) {
            currentUser.viewWorkoutPlan();
        } else if (choice == JOptionPane.NO_OPTION) {
            currentUser.viewDietChart();
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new OnlinePersonalTrainingAssistant());
    }
}

class UserInterface extends JPanel {
    private OnlinePersonalTrainingAssistant assistant;
    private JButton authenticateButton;

    public UserInterface(OnlinePersonalTrainingAssistant assistant) {
        this.assistant = assistant;

        authenticateButton = new JButton("Authenticate User");
        authenticateButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String name = JOptionPane.showInputDialog("Enter your name:");
                double weight = Double.parseDouble(JOptionPane.showInputDialog("Enter your weight (kg):"));
                double height = Double.parseDouble(JOptionPane.showInputDialog("Enter your height (cm):"));

                assistant.authenticateUser(name, weight, height);
            }
        });

        add(authenticateButton);
    }
}
