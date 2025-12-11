import java.awt.*;
import java.awt.event.*;
import java.util.*;

class Ambulance {
    private String id;
    private String driver;
    private boolean available;
    private String location;
    
    public Ambulance(String id, String driver, String location) {
        this.id = id;
        this.driver = driver;
        this.location = location;
        this.available = true;
    }
    
    public String getId() { return id; }
    public String getDriver() { return driver; }
    public boolean isAvailable() { return available; }
    public String getLocation() { return location; }
    
    public void setAvailable(boolean available) { this.available = available; }
    public void setLocation(String location) { this.location = location; }
    
    public String toString() {
        return id + " - " + driver + " - " + location + " - " + (available ? "Available" : "Busy");
    }
}

class Emergency {
    private String id;
    private String patient;
    private String location;
    private String type;
    private String status;
    private String ambulanceId;
    private boolean sos;
    
    public Emergency(String patient, String location, String type) {
        this.id = "REQ" + System.currentTimeMillis();
        this.patient = patient;
        this.location = location;
        this.type = type;
        this.status = "PENDING";
        this.ambulanceId = "None";
        this.sos = false;
    }
    
    public Emergency() {
        this.id = "SOS" + System.currentTimeMillis();
        this.patient = "Emergency Patient";
        this.location = "Unknown Location";
        this.type = "CRITICAL SOS";
        this.status = "PENDING";
        this.ambulanceId = "None";
        this.sos = true;
    }
    
    public String getId() { return id; }
    public String getPatient() { return patient; }
    public String getLocation() { return location; }
    public String getType() { return type; }
    public String getStatus() { return status; }
    public String getAmbulanceId() { return ambulanceId; }
    public boolean isSOS() { return sos; }
    
    public void setStatus(String status) { this.status = status; }
    public void setAmbulanceId(String ambulanceId) { this.ambulanceId = ambulanceId; }
    
    public String toString() {
        return (sos ? "SOS " : "") + id + " - " + patient + " - " + location + " - " + type + " - " + status;
    }
}

public class AmbulanceManagementSystem extends Frame {
    private ArrayList<Ambulance> ambulances = new ArrayList<>();
    private ArrayList<Emergency> emergencies = new ArrayList<>();
    private TextArea display;
    private TextField idField, driverField, locField;
    private TextField patientField, emergLocField, typeField;
    
    public AmbulanceManagementSystem() {
        setupData();
        createWindow();
    }
    
    private void setupData() {
        ambulances.add(new Ambulance("AMB001", "John Doe", "Downtown"));
        ambulances.add(new Ambulance("AMB002", "Jane Smith", "Uptown"));
        ambulances.add(new Ambulance("AMB003", "Mike Johnson", "Suburb"));
    }
    
    private void createWindow() {
        setTitle("Ambulance Management System");
        setSize(800, 600);
        setLayout(new BorderLayout());
        
        // Header
        Panel header = new Panel();
        header.setBackground(Color.BLUE);
        Label title = new Label("AMBULANCE MANAGEMENT SYSTEM", Label.CENTER);
        title.setFont(new Font("Arial", Font.BOLD, 18));
        title.setForeground(Color.WHITE);
        header.add(title);
        add(header, BorderLayout.NORTH);
        
        // Main content
        Panel main = new Panel();
        main.setLayout(new GridLayout(1, 2));
        
        // Left side - Inputs
        Panel left = new Panel();
        left.setLayout(new GridLayout(3, 1));
        
        // SOS Panel
        Panel sosPanel = new Panel();
        sosPanel.setBackground(new Color(255, 200, 200));
        Button sosBtn = new Button("SOS - SEND AMBULANCE NOW!");
        sosBtn.setBackground(Color.RED);
        sosBtn.setForeground(Color.WHITE);
        sosBtn.setFont(new Font("Arial", Font.BOLD, 14));
        sosPanel.add(sosBtn);
        sosBtn.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                createSOS();
            }
        });
        
        // Ambulance Panel
        Panel ambPanel = new Panel();
        ambPanel.setLayout(new GridLayout(4, 2));
        ambPanel.add(new Label("Ambulance ID:"));
        idField = new TextField();
        ambPanel.add(idField);
        ambPanel.add(new Label("Driver Name:"));
        driverField = new TextField();
        ambPanel.add(driverField);
        ambPanel.add(new Label("Location:"));
        locField = new TextField();
        ambPanel.add(locField);
        Button addBtn = new Button("Add Ambulance");
        addBtn.setBackground(Color.GREEN);
        addBtn.setForeground(Color.WHITE);
        ambPanel.add(new Label(""));
        ambPanel.add(addBtn);
        addBtn.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                addAmbulance();
            }
        });
        
        // Emergency Panel
        Panel emergPanel = new Panel();
        emergPanel.setLayout(new GridLayout(4, 2));
        emergPanel.add(new Label("Patient Name:"));
        patientField = new TextField();
        emergPanel.add(patientField);
        emergPanel.add(new Label("Location:"));
        emergLocField = new TextField();
        emergPanel.add(emergLocField);
        emergPanel.add(new Label("Emergency Type:"));
        typeField = new TextField();
        emergPanel.add(typeField);
        Button emergBtn = new Button("Create Emergency");
        emergBtn.setBackground(Color.RED);
        emergBtn.setForeground(Color.WHITE);
        emergPanel.add(new Label(""));
        emergPanel.add(emergBtn);
        emergBtn.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                createEmergency();
            }
        });
        
        left.add(sosPanel);
        left.add(ambPanel);
        left.add(emergPanel);
        
        // Right side - Display
        Panel right = new Panel();
        right.setLayout(new BorderLayout());
        display = new TextArea(20, 40);
        display.setEditable(false);
        Panel displayHeader = new Panel();
        displayHeader.setBackground(Color.BLUE);
        Label displayLabel = new Label("System Output", Label.CENTER);
        displayLabel.setForeground(Color.WHITE);
        displayHeader.add(displayLabel);
        right.add(displayHeader, BorderLayout.NORTH);
        right.add(display, BorderLayout.CENTER);
        
        main.add(left);
        main.add(right);
        add(main, BorderLayout.CENTER);
        
        // Bottom buttons
        Panel bottom = new Panel();
        Button viewAmbBtn = new Button("View Ambulances");
        Button viewEmergBtn = new Button("View Emergencies");
        Button assignBtn = new Button("Auto Assign");
        Button exitBtn = new Button("Exit");
        
        viewAmbBtn.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                showAmbulances();
            }
        });
        
        viewEmergBtn.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                showEmergencies();
            }
        });
        
        assignBtn.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                autoAssign();
            }
        });
        
        exitBtn.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                System.exit(0);
            }
        });
        
        bottom.add(viewAmbBtn);
        bottom.add(viewEmergBtn);
        bottom.add(assignBtn);
        bottom.add(exitBtn);
        add(bottom, BorderLayout.SOUTH);
        
        // Window listener
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
        
        centerWindow();
        setVisible(true);
    }
    
    private void centerWindow() {
        Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
        Dimension windowSize = getSize();
        int x = (screenSize.width - windowSize.width) / 2;
        int y = (screenSize.height - windowSize.height) / 2;
        setLocation(x, y);
    }
    
    private void createSOS() {
        Emergency sos = new Emergency();
        ArrayList<Ambulance> available = new ArrayList<>();
        for (Ambulance amb : ambulances) {
            if (amb.isAvailable()) available.add(amb);
        }
        
        if (available.isEmpty()) {
            emergencies.add(sos);
            display.setText("SOS EMERGENCY REGISTERED!\n\nRequest ID: " + sos.getId() + 
                           "\nStatus: No ambulances available immediately!\nWe are searching for available unit...");
        } else {
            Ambulance amb = available.get(0);
            amb.setAvailable(false);
            sos.setStatus("ASSIGNED - HIGH PRIORITY");
            sos.setAmbulanceId(amb.getId());
            emergencies.add(sos);
            display.setText("SOS EMERGENCY RESPONSE ACTIVATED!\n\n" +
                           "Request ID: " + sos.getId() + "\n" +
                           "Assigned Ambulance: " + amb.getId() + "\n" +
                           "Driver: " + amb.getDriver() + "\n" +
                           "Status: EMERGENCY DEPLOYMENT\n\n" +
                           "AMBULANCE IS RUSHING TO YOUR LOCATION!\nETA: 3-5 minutes");
        }
    }
    
    private void addAmbulance() {
        String id = idField.getText().trim();
        String driver = driverField.getText().trim();
        String loc = locField.getText().trim();
        
        if (id.isEmpty() || driver.isEmpty() || loc.isEmpty()) {
            display.setText("Error: Please fill all fields for ambulance!");
            return;
        }
        
        for (Ambulance amb : ambulances) {
            if (amb.getId().equals(id)) {
                display.setText("Error: Ambulance ID " + id + " already exists!");
                return;
            }
        }
        
        ambulances.add(new Ambulance(id, driver, loc));
        idField.setText(""); 
        driverField.setText(""); 
        locField.setText("");
        display.setText("Ambulance " + id + " added successfully!\nDriver: " + driver + "\nLocation: " + loc);
    }
    
    private void createEmergency() {
        String patient = patientField.getText().trim();
        String loc = emergLocField.getText().trim();
        String type = typeField.getText().trim();
        
        if (patient.isEmpty() || loc.isEmpty() || type.isEmpty()) {
            display.setText("Error: Please fill all fields for emergency request!");
            return;
        }
        
        Emergency emerg = new Emergency(patient, loc, type);
        emergencies.add(emerg);
        patientField.setText(""); 
        emergLocField.setText(""); 
        typeField.setText("");
        display.setText("Emergency request created successfully!\n\n" +
                       "Request ID: " + emerg.getId() + "\n" +
                       "Patient: " + patient + "\n" +
                       "Location: " + loc + "\n" +
                       "Emergency Type: " + type);
    }
    
    private void showAmbulances() {
        StringBuilder sb = new StringBuilder();
        sb.append("=== ALL AMBULANCES ===\n\n");
        
        if (ambulances.isEmpty()) {
            sb.append("No ambulances available.\n");
        } else {
            for (int i = 0; i < ambulances.size(); i++) {
                Ambulance ambulance = ambulances.get(i);
                sb.append((i + 1) + ". " + ambulance.toString() + "\n");
            }
        }
        
        sb.append("\nTotal Ambulances: " + ambulances.size());
        sb.append("\nAvailable: " + countAvailable());
        
        display.setText(sb.toString());
    }
    
    private void showEmergencies() {
        StringBuilder sb = new StringBuilder();
        sb.append("=== ALL EMERGENCY REQUESTS ===\n\n");
        
        if (emergencies.isEmpty()) {
            sb.append("No emergency requests.\n");
        } else {
            for (int i = 0; i < emergencies.size(); i++) {
                Emergency request = emergencies.get(i);
                sb.append((i + 1) + ". " + request.toString() + "\n");
                sb.append("   Assigned Ambulance: " + request.getAmbulanceId() + "\n\n");
            }
        }
        
        sb.append("Total Requests: " + emergencies.size());
        sb.append("\nPending: " + countPending());
        sb.append("\nSOS Emergencies: " + countSOS());
        
        display.setText(sb.toString());
    }
    
    private void autoAssign() {
        int assignedCount = 0;
        
        ArrayList<Emergency> pendingRequests = new ArrayList<>();
        for (Emergency request : emergencies) {
            if ("PENDING".equals(request.getStatus())) {
                pendingRequests.add(request);
            }
        }
        
        if (pendingRequests.isEmpty()) {
            display.setText("No pending emergency requests available for assignment.");
            return;
        }
        
        ArrayList<Ambulance> availableAmbulances = new ArrayList<>();
        for (Ambulance ambulance : ambulances) {
            if (ambulance.isAvailable()) {
                availableAmbulances.add(ambulance);
            }
        }
        
        if (availableAmbulances.isEmpty()) {
            display.setText("No available ambulances at the moment!");
            return;
        }
        
        int maxAssignments = Math.min(availableAmbulances.size(), pendingRequests.size());
        for (int i = 0; i < maxAssignments; i++) {
            Emergency request = pendingRequests.get(i);
            Ambulance ambulance = availableAmbulances.get(i);
            
            ambulance.setAvailable(false);
            request.setStatus("ASSIGNED");
            request.setAmbulanceId(ambulance.getId());
            assignedCount++;
        }
        
        display.setText("Auto-assignment completed!\n" +
                       "Assigned " + assignedCount + " ambulances to pending emergencies.");
    }
    
    private int countAvailable() {
        int count = 0;
        for (Ambulance ambulance : ambulances) {
            if (ambulance.isAvailable()) {
                count++;
            }
        }
        return count;
    }
    
    private int countPending() {
        int count = 0;
        for (Emergency request : emergencies) {
            if ("PENDING".equals(request.getStatus())) {
                count++;
            }
        }
        return count;
    }
    
    private int countSOS() {
        int count = 0;
        for (Emergency request : emergencies) {
            if (request.isSOS()) {
                count++;
            }
        }
        return count;
    }
    
    public static void main(String[] args) {
        new AmbulanceManagementSystem();
    }
}
