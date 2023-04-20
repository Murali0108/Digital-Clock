import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.Graphics;
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
import java.util.concurrent.TimeUnit;
import javax.swing.JFrame;
import javax.swing.JPanel;

public class digitalclock {
    public static void main(String[] args) throws InterruptedException {
        JFrame frame = new JFrame();
        ClockPanel panel = new ClockPanel();
        frame.add(panel);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.pack();
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
        while (true) {
            LocalTime time = LocalTime.now();
            LocalDate date = LocalDate.now();
            String formattedTime = time.format(DateTimeFormatter.ofPattern("HH:mm:ss"));
            String formattedWeekday = date.format(DateTimeFormatter.ofPattern("EEEE"));
            String formattedMonth = date.format(DateTimeFormatter.ofPattern("MMMM"));
            String formattedYear = date.format(DateTimeFormatter.ofPattern("yyyy"));
            panel.setTime(formattedWeekday, formattedMonth, formattedYear, formattedTime);
            TimeUnit.SECONDS.sleep(1);
            panel.repaint();
        }
    }
}

class ClockPanel extends JPanel {
    private String time;
    private String weekday;
    private String month;
    private String year;

    public ClockPanel() {
        setPreferredSize(new Dimension(400, 150));
        setBackground(Color.BLACK);
        setFont(new Font("Arial", Font.BOLD, 36));
        setForeground(Color.GREEN);
    }

    public void setTime(String weekday, String month, String year, String time) {
        this.weekday = weekday;
        this.month = month;
        this.year = year;
        this.time = time;
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        g.drawString(weekday, 50, 50);
        g.drawString(month, 50, 90);
        g.drawString(year, 50, 130);
        g.drawString(time, 200, 90);
    }
}
