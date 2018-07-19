---
date : 07-17
Le : Key Listener
---



```java
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import javax.swing.JFrame;

public class Exam extends JFrame implements KeyListner {

  public Exam {
    super("title");

    setLayout(null);
    setResizable(false);
    setIconImage(Toolkit.getDefaultToolkit().getImage("filesrc"));	// FAVICON
    setVisible(true);
    setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

    addKeyListener(this);	// Frame 에 KeyListener 호출.        
  }
  // Exam ends;

  public void pain(Graphics g) {

  }
	// pain ends;
  
  @Override
  public void keyPressed(KeyEvent e) {
    int key = e.getKeyCode();	// 자판값 인식.
  }
  public void keyReleased(KeyEvent e) {
    
  }
  public void keyTyped(KeyEvent e) {
    
  }
  
  
  public static void main(String[] args) {
    new Exam();	// executable.
  }  


}



```



-   `g.clearRact(x: 0, y: 0);`	// 프레임창 초기화

    `g.drawImage(x,y);`	// 초기 이미지 좌표 설정.

-   `repaint();`   // 그림 다시 부르기. keyPressed()

-   keyEvent.VK_RIGHT, VK_LEFT....

    