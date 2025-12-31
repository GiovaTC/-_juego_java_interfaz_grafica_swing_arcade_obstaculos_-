# -_juego_java_interfaz_grafica_swing_arcade_obstaculos_- :. 
## 🎮 Juego Java con Interfaz Gráfica (Swing) – Arcade con Obstaculos .

<img width="260" height="90" alt="image" src="https://github.com/user-attachments/assets/899972cf-e9c3-4e25-b6ac-fe7c485cdac6" />  

A continuación tienes una solución completa, profesional y lista para ejecutar en IntelliJ IDEA, para un juego en Java con interfaz gráfica (Swing) .
Es un minijuego tipo arcade: el usuario mueve un cuadrado rojo y debe evitar chocar con obstáculos que se mueven. Incluye lógica de colisiones, marcador y estructura ordenada .

## ✔️ Características del Juego

Java + IntelliJ IDEA

Interfaz gráfica (Swing – JFrame / JPanel)

Movimiento con teclas (↑ ↓ ← →)

Obstáculos en movimiento

Detección de colisiones

Game Over con reinicio

Código simple, claro y mantenible

## 1️⃣ Requerimientos

IntelliJ IDEA

JDK 8+

No requiere librerías externas.

## 2️⃣ Código Completo (copiar y ejecutar)
➤ Clase principal: GameMain.java
import javax.swing.*;

public class GameMain {

    public static void main(String[] args) {
        JFrame frame = new JFrame("Juego Java - Interfaz Gráfica");
        GamePanel panel = new GamePanel();

        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setResizable(false);
        frame.add(panel);
        frame.pack();
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}

➤ Lógica del juego: GamePanel.java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;
import java.util.Random;

public class GamePanel extends JPanel implements ActionListener, KeyListener {

    private Timer timer;
    private int playerX = 50, playerY = 200;
    private final int PLAYER_SIZE = 40;
    private int score = 0;
    private boolean gameOver = false;

    private ArrayList<Rectangle> obstacles;
    private Random random;

    public GamePanel() {
        this.setPreferredSize(new Dimension(800, 400));
        this.setBackground(Color.BLACK);
        this.setFocusable(true);
        this.addKeyListener(this);

        obstacles = new ArrayList<>();
        random = new Random();

        generateObstacle();

        timer = new Timer(20, this);
        timer.start();
    }

    private void generateObstacle() {
        int height = 50 + random.nextInt(100);
        int y = random.nextInt(300);
        obstacles.add(new Rectangle(800, y, 40, height));
    }

    @Override
    public void paintComponent(Graphics g) {
        super.paintComponent(g);

        // Jugador
        g.setColor(Color.RED);
        g.fillRect(playerX, playerY, PLAYER_SIZE, PLAYER_SIZE);

        // Obstáculos
        g.setColor(Color.GREEN);
        for (Rectangle rect : obstacles) {
            g.fillRect(rect.x, rect.y, rect.width, rect.height);
        }

        // Marcador
        g.setColor(Color.WHITE);
        g.setFont(new Font("Arial", Font.BOLD, 20));
        g.drawString("Puntos: " + score, 10, 20);

        // Game Over
        if (gameOver) {
            g.setFont(new Font("Arial", Font.BOLD, 40));
            g.setColor(Color.YELLOW);
            g.drawString("GAME OVER", 280, 200);
            g.setFont(new Font("Arial", Font.PLAIN, 20));
            g.drawString("Presiona ENTER para reiniciar", 270, 240);
        }
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (!gameOver) {
            moveObstacles();
            checkCollision();
            repaint();
        }
    }

    private void moveObstacles() {
        for (Rectangle rect : obstacles) {
            rect.x -= 5;
        }

        if (obstacles.get(obstacles.size() - 1).x < 500) {
            generateObstacle();
        }

        if (obstacles.get(0).x + obstacles.get(0).width < 0) {
            obstacles.remove(0);
            score++;
        }
    }

    private void checkCollision() {
        Rectangle player = new Rectangle(playerX, playerY, PLAYER_SIZE, PLAYER_SIZE);

        for (Rectangle rect : obstacles) {
            if (player.intersects(rect)) {
                gameOver = true;
                timer.stop();
            }
        }
    }

    private void restartGame() {
        playerX = 50;
        playerY = 200;
        score = 0;
        gameOver = false;
        obstacles.clear();
        generateObstacle();
        timer.start();
    }

    @Override
    public void keyPressed(KeyEvent e) {
        if (!gameOver) {
            switch (e.getKeyCode()) {
                case KeyEvent.VK_UP -> playerY -= 10;
                case KeyEvent.VK_DOWN -> playerY += 10;
                case KeyEvent.VK_LEFT -> playerX -= 10;
                case KeyEvent.VK_RIGHT -> playerX += 10;
            }
        } else if (e.getKeyCode() == KeyEvent.VK_ENTER) {
            restartGame();
        }
        repaint();
    }

    @Override public void keyReleased(KeyEvent e) {}
    @Override public void keyTyped(KeyEvent e) {}
}

## ▶️ Cómo ejecutarlo en IntelliJ IDEA

* 1️⃣ Crear un nuevo proyecto Java.
* 2️⃣ Crear el archivo GameMain.java.
* 3️⃣ Crear el archivo GamePanel.java.
* 4️⃣ Ejecutar GameMain . :. .
