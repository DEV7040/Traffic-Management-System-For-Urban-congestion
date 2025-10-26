import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;

public class TrafficGUI extends JFrame {
    private LanePanel[] lanes = new LanePanel[4];
    private JButton emergencyBtn = new JButton("Emergency Vehicle!");
    private Timer simulationTimer;
    private Random rand = new Random();

    public TrafficGUI() {
        setTitle("Traffic Management Simulation");
        setSize(600, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        JPanel lanesPanel = new JPanel();
        lanesPanel.setLayout(new GridLayout(1, 4, 10, 10));

        for (int i = 0; i < 4; i++) {
            lanes[i] = new LanePanel("Lane " + (i + 1));
            lanesPanel.add(lanes[i]);
        }

        add(lanesPanel, BorderLayout.CENTER);
        add(emergencyBtn, BorderLayout.SOUTH);

        emergencyBtn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("🚨 Emergency vehicle detected! Lane 1 priority.");
                lanes[0].givePriority();
            }
        });

        // Simulation timer - every 1 second
        simulationTimer = new Timer(1000, new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                simulateTraffic();
            }
        });
        simulationTimer.start();
    }

    private void simulateTraffic() {
        // Randomly add vehicles
        for (LanePanel lane : lanes) {
            if (rand.nextInt(10) < 3) lane.addVehicle();
        }

        // Check lanes
        for (LanePanel lane : lanes) {
            lane.updateTraffic();
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            TrafficGUI gui = new TrafficGUI();
            gui.setVisible(true);
        });
    }

    // Inner class for each lane panel
    class LanePanel extends JPanel {
        private String name;
        private int vehicles = 0;
        private long lastGreenTime = System.currentTimeMillis();
        private long maxWait = 60000; // 60 sec
        private long defaultGreen = 5000; // 5 sec
        private Color lightColor = Color.RED;
        private long greenStartTime = 0;
        private boolean greenActive = false;

        public LanePanel(String name) {
            this.name = name;
            setPreferredSize(new Dimension(100, 300));
            setBackground(Color.LIGHT_GRAY);
        }

        public void addVehicle() {
            vehicles++;
        }

        public void givePriority() {
            greenActive = true;
            greenStartTime = System.currentTimeMillis();
            lightColor = Color.GREEN;
            vehicles = 0;
            repaint();
        }

        public void updateTraffic() {
            long now = System.currentTimeMillis();
            if (!greenActive) {
                if (vehicles > 0) {
                    // Vehicle detected → instant green
                    greenActive = true;
                    greenStartTime = now;
                    lightColor = Color.GREEN;
                    vehicles = 0;
                    System.out.println(name + " vehicle detected. GREEN light ON.");
                } else if (now - lastGreenTime >= maxWait) {
                    // Max wait override
                    greenActive = true;
                    greenStartTime = now;
                    lightColor = Color.GREEN;
                    System.out.println(name + " waited too long. GREEN light ON.");
                }
            } else {
                // Green active → check duration
                if (now - greenStartTime >= defaultGreen) {
                    greenActive = false;
                    lastGreenTime = now;
                    lightColor = Color.RED;
                    System.out.println(name + " GREEN ended. RED light ON.");
                }
            }
            repaint();
        }

        @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            g.setColor(Color.BLACK);
            g.drawString(name + " Vehicles: " + vehicles, 10, 20);

            // Draw traffic light circles
            g.setColor(Color.RED);
            g.fillOval(40, 50, 40, 40);

            g.setColor(Color.YELLOW);
            g.fillOval(40, 100, 40, 40);

            g.setColor(lightColor);
            g.fillOval(40, 150, 40, 40);
        }
    }
}
