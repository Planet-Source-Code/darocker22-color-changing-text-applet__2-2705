<div align="center">

## Color changing text applet


</div>

### Description

This is a cool text chaning color applet. You can type any text and it'll fade the color.
 
### More Info
 
<APPLET CODE="GradBlink.class" WIDTH=400 HEIGHT=50>

<PARAM NAME="message" VALUE="Planet-Source-Code.com">

<PARAM NAME="speed" VALUE="20">

<PARAM NAME="bgColor" VALUE="#000000">

<PARAM NAME="align" VALUE="center">

<PARAM NAME="font" VALUE="Arial">

<PARAM NAME="style" VALUE="bold">

<PARAM NAME="size" VALUE="30">

</APPLET>


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[darocker22](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/darocker22.md)
**Level**          |Intermediate
**User Rating**    |5.0 (20 globes from 4 users)
**Compatibility**  |Java \(JDK 1\.2\)
**Category**       |[Applet](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/applet__2-81.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/darocker22-color-changing-text-applet__2-2705/archive/master.zip)





### Source Code

```

import java.awt.Color;
class CycleColor
{
  int MAX_RGB;
  int COLOR_CYCLE;
  int CYCLE_STEP;
  int hue;
  public CycleColor()
  {
    MAX_RGB = 255;
    COLOR_CYCLE = 6 * MAX_RGB;
    CYCLE_STEP = COLOR_CYCLE / 250;
    hue = (int)(Math.random() * (double)COLOR_CYCLE);
  }
  public void step()
  {
    hue = (hue + CYCLE_STEP) % COLOR_CYCLE;
  }
  public Color color()
  {
    int i = triad_value(0);
    int j = triad_value(4 * MAX_RGB);
    int k = triad_value(2 * MAX_RGB);
    return new Color(i, j, k);
  }
  private int triad_value(int i)
  {
    int j = (hue + i) % COLOR_CYCLE;
    if(j > 3 * MAX_RGB)
    {
      j = Math.abs(j - COLOR_CYCLE);
    }
    if(j <= MAX_RGB)
    {
      return MAX_RGB;
    }
    if(j <= 2 * MAX_RGB)
    {
      return MAX_RGB - (j - MAX_RGB);
    }
    else
    {
      return 0;
    }
  }
}
//#####################
import java.applet.Applet;
import java.awt.*;
public class GradBlink extends Applet
  implements Runnable
{
  Thread blinker;
  String lbl;
  String align;
  Font font;
  int iFontStyle;
  int iFontSize;
  int speed;
  int x;
  int y;
  Dimension d;
  CycleColor color;
  boolean bSfondo;
  public void init()
  {
    color = new CycleColor();
    d = size();
    String s = getParameter("style");
    if(s.equalsIgnoreCase("plain"))
    {
      iFontStyle = 0;
    }
    else if(s.equalsIgnoreCase("bold"))
    {
      iFontStyle = 1;
    }
    else if(s.equalsIgnoreCase("italic"))
    {
      iFontStyle = 2;
    }
    else
    {
      iFontStyle = 0;
    }
    s = getParameter("size");
    iFontSize = s != null ? Integer.valueOf(s).intValue() : 24;
    s = getParameter("font");
    font = s != null ? new Font(s, iFontStyle, iFontSize) : new Font("TimesRoman", 0, 24);
    s = getParameter("speed");
    speed = s != null ? 1000 / Integer.valueOf(s).intValue() : 400;
    s = getParameter("message");
    lbl = s != null ? s : "Text Gradient";
    Color color1 = TransColor(getParameter("bgColor"), getBackground());
    setBackground(color1);
    align = getParameter("align");
  }
  public void paint(Graphics g)
  {
    int i = 0;
    int j = font.getSize();
    g.setFont(font);
    i = StringYPosition(g, lbl);
    color.step();
    g.setColor(color.color());
    g.drawString(lbl, i, j);
  }
  public void update(Graphics g)
  {
    paint(g);
  }
  public boolean mouseDown(Event event, int i, int j)
  {
    String s = "Created by Gian Luca Farina Perseu on 12 Feb. 1996. email: perseu@comune.torino.it";
    showStatus(s);
    return true;
  }
  public int StringYPosition(Graphics g, String s)
  {
    int i = 0;
    int j = 0;
    j = g.getFontMetrics().stringWidth(s);
    if(j > size().width)
    {
      j = size().width;
    }
    if(align.equalsIgnoreCase("left"))
    {
      i = 0;
    }
    else if(align.equalsIgnoreCase("center"))
    {
      i = (size().width - j) / 2;
    }
    else if(align.equalsIgnoreCase("right"))
    {
      i = size().width - j;
    }
    return i;
  }
  public void start()
  {
    blinker = new Thread(this);
    blinker.start();
  }
  public void stop()
  {
    blinker.stop();
  }
  public void run()
  {
    do
    {
      try
      {
        Thread.currentThread();
        Thread.sleep(speed);
      }
      catch(InterruptedException _ex) { }
      repaint();
    } while(true);
  }
  public Color TransColor(String s, Color color1)
  {
    if(s == null || s.charAt(0) != '#' || s.length() != 7)
    {
      return color1;
    }
    try
    {
      Integer integer = new Integer(0);
      integer = Integer.valueOf(s.substring(1, 7), 16);
      return new Color(integer.intValue());
    }
    catch(Exception _ex)
    {
      return color1;
    }
  }
  public GradBlink()
  {
    bSfondo = false;
  }
}
```

