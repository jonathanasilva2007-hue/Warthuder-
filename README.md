# Warthuder-
Tanks
package pelotaowar;
import robocode.*;
import java.awt.Color;

public class LiderWar extends TeamRobot {
    public void run() {
        // Cores personalizadas do tanque
        setBodyColor(Color.BLUE);
        setGunColor(Color.DARK_GRAY);
        setRadarColor(Color.WHITE);

        // Comportamento autônomo de patrulha e varredura do mapa[span_4](start_span)[span_4](end_span)
        while (true) {
            turnRadarRight(360);
            ahead(60);
            turnRadarRight(360);
            back(60);
        }
    }

    public void onScannedRobot(ScannedRobotEvent e) {
        // Verifica se o robô avistado NÃO é um aliado do time[span_5](start_span)[span_5](end_span)
        if (!isTeammate(e.getName())) {
            try {
                // Empacota os dados do inimigo (direção, distância e energia) e envia para o time[span_6](start_span)[span_6](end_span)
                double[] dadosInimigo = { e.getBearing(), e.getDistance(), e.getEnergy() };
                broadcastMessage(dadosInimigo);
            } catch (Exception ex) {
                ex.printStackTrace();
            }
            // O líder também atira para enfraquecer o oponente[span_7](start_span)[span_7](end_span)
            fire(1);
        }
    }

    public void onHitByBullet(HitByBulletEvent e) {
        back(30); // Recua ao tomar um tiro[span_8](start_span)[span_8](end_span)
    }

    public void onHitWall(HitWallEvent e) {
        turnRight(90);
        ahead(50); // Desvia da parede[span_9](start_span)[span_9](end_span)
    }
}
