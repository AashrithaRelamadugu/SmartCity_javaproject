# SmartCity_javaproject
/*Smart City is a web-based application built using Java. It stores details of a city and displays information about the city such as hotels, shopping marts, restaurants, tourist places, transportation modes, and also some general info. This acts as a guide to the new visitors.*/
import java.awt.*;
import javax.swing.*;

public class SmartCityApp {
    public static void main(String[] args) {
        new SignUpPage();
    }
}

class SignUpPage extends JFrame {
    private JTextField nameField, emailField, cityField;
    private JButton signUpButton;

    public SignUpPage() {
        setTitle("Sign Up");
        setSize(240, 150); // Reduced size
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(4, 2, 3, 3)); // Compact spacing

        JLabel nameLabel = new JLabel("Name:");
        nameLabel.setHorizontalAlignment(SwingConstants.CENTER);
        add(nameLabel);

        nameField = new JTextField();
        nameField.setFont(new Font("Arial", Font.PLAIN, 10));
        add(nameField);

        JLabel emailLabel = new JLabel("Email:");
        emailLabel.setHorizontalAlignment(SwingConstants.CENTER);
        add(emailLabel);

        emailField = new JTextField();
        emailField.setFont(new Font("Arial", Font.PLAIN, 10));
        add(emailField);

        JLabel cityLabel = new JLabel("City:");
        cityLabel.setHorizontalAlignment(SwingConstants.CENTER);
        add(cityLabel);

        cityField = new JTextField();
        cityField.setFont(new Font("Arial", Font.PLAIN, 10));
        add(cityField);

        signUpButton = new JButton("Sign Up");
        signUpButton.setFont(new Font("Arial", Font.BOLD, 10));
        add(new JLabel()); // Spacer
        add(signUpButton);

        signUpButton.addActionListener(e -> {
            String name = nameField.getText();
            String city = cityField.getText();

            if (name.isEmpty() || city.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Please fill all fields", "Error", JOptionPane.ERROR_MESSAGE);
            } else {
                new Dashboard(name, city);
                dispose();
            }
        });

        setVisible(true);
    }
}

class Dashboard extends JFrame {
    public Dashboard(String userName, String city) {
        setTitle("Dashboard");
        setSize(320, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout(5, 5));

        JLabel welcomeLabel = new JLabel("Welcome, " + userName + "! Current City: " + city, JLabel.CENTER);
        welcomeLabel.setFont(new Font("Arial", Font.BOLD, 12));
        add(welcomeLabel, BorderLayout.NORTH);

        JPanel buttonPanel = new JPanel(new GridLayout(1, 3, 3, 3));

        JButton businessButton = new JButton("Business");
        JButton studentButton = new JButton("Students");
        JButton touristButton = new JButton("Tourists");

        businessButton.setFont(new Font("Arial", Font.PLAIN, 10));
        studentButton.setFont(new Font("Arial", Font.PLAIN, 10));
        touristButton.setFont(new Font("Arial", Font.PLAIN, 10));

        buttonPanel.add(businessButton);
        buttonPanel.add(studentButton);
        buttonPanel.add(touristButton);

        add(buttonPanel, BorderLayout.CENTER);

        businessButton.addActionListener(e -> showPlaces("Business People",
                new String[]{"Conference Centers", "Co-working Spaces", "Hotels"}));
        studentButton.addActionListener(e -> showPlaces("Students",
                new String[]{"Libraries", "Universities", "Cafes"}));
        touristButton.addActionListener(e -> showPlaces("Tourists",
                new String[]{"Museums", "Parks", "Historical Monuments"}));

        JButton exitButton = new JButton("Exit");
        exitButton.setFont(new Font("Arial", Font.BOLD, 10));
        exitButton.addActionListener(e -> System.exit(0));
        add(exitButton, BorderLayout.SOUTH);

        setVisible(true);
    }

    private void showPlaces(String category, String[] places) {
        StringBuilder message = new StringBuilder("Places for " + category + ":\n");
        for (String place : places) {
            message.append("- ").append(place).append("\n");
        }
        JOptionPane.showMessageDialog(this, message.toString(), category + " Places", JOptionPane.INFORMATION_MESSAGE);
    }
}

