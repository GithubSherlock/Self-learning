# 5_Repräsentation von Farbe

Created: July 13, 2023 3:19 PM

# 5_Repräsentation von Farbe

# 5.1 Additive/Subtraktive Farbmischung

- Anwenungsbeispiel
    - Additive
        - Bildschirm
    - Substrative
        - Drücken
    
    <aside>
    💡 **Was passiert bei additiver/subtraktiver Farbmischung?**
    
    Additiv: durch das Hinzufügen von Licht erzeugt
    
    Subtraktiv: durch das Absorbieren von Licht erzeugt
    
    </aside>
    
    ![Untitled](5_Repra%CC%88sentation%20von%20Farbe/Untitled.png)
    

## 5.2 Farbempfinden und technische Repräsentation von Farbe

<aside>
💡 Untersuchung: **Warum reichen 3 Farben zur Repräsentation eines gesamten Spektrums?**

Ergebnis der Experimente:

- Für die meisten Probanden galt
    - Testsignale konnte mit 3 Grundfarben repräsentiert werden
    - Eingestellte Gewichtungen wR, wG, wB für eine Testfarbe bei den Probanden nahezu identisch
    - Subtraktive Farbmischung war notwendig
- Menschliches Farbempfinden durch Überlagerung von 3 Grundfarben im Bild darstellbar (3 unterschiedliche Zelltypen für Farbinformationen)
- Ableitung einer Spektralwertfunktion für Repräsentation von Farbe mit den Grundfarben R, G, B
</aside>

- **Spektralwertfunktion**
  
    $$
    E[S]=\omega_R \cdot R + \omega_G \cdot G + \omega_B \cdot B
    $$
    
    $E[S]$ - Farbempfindung
    
    $\omega_R,\omega_G,\omega_B$ - Wichtung der 3 Farbkomponenten (experimentall)
    
    $f_R,f_G,f_B$ - Spektralwertfunktion
    
    $S(\lambda)$ - Spektrum der Lichtquelle
    
    Diagramm zeigt die Spektralwertfunktionen:
    
    ![截屏2023-06-14 16.00.17.png](5_Repra%CC%88sentation%20von%20Farbe/%25E6%2588%25AA%25E5%25B1%258F2023-06-14_16.00.17.png)
    
- **Definition Normspektralwertfunktion**
  
    ![Untitled](5_Repra%CC%88sentation%20von%20Farbe/Untitled%201.png)
    
    Normspektralwertfunktion in (b) → Vermeidung negativer Werte
    
- **Normfarbwerte**
  
    ![Untitled](5_Repra%CC%88sentation%20von%20Farbe/Untitled%202.png)
    
    > **Beschreibung:**
    > 
    > 
    > 视网膜中图像的灰度光谱值分别乘以红绿蓝三色的光谱值，苹果的图像光谱中红色的面积居多，所以看到的以红色为主
    > 
- **Normfarbtafel nach CIE**
  
    [CIE 1931色彩空间 - 维基百科，自由的百科全书](https://zh.wikipedia.org/zh-cn/CIE_1931色彩空间)
    
    $$
    \begin{align*}
    x&=\frac{X}{X+Y+Z}\\
    y&=\frac{Y}{X+Y+Z}\\
    z&=\frac{Z}{X+Y+Z}
    \end{align*}
    $$
    
    - jeder Punkt des Diagramms repräsentiert eine Farbe,
    - alle Farben auf der Strecke zwischen zwei Farbpunkten können durch Mischen der Farben der Endpunkte hergestellt werden,
    - alle Punkte innerhalb eines Dreiecks sind durch Mischen der Farben der Eckpunkte zu erhalten.
- **Technische Repräsentation von Farbe**
    - In der Regel durch 3 numerische Werte - 3 Farbkanäle
    - Aber auch Multispektralbilder - N Farbkanäle
    - Digitale Bildverarbeitung: Jedes Pixel ist ein Vektor mit 3 (bzw. N) Komponenten
    - Nachfolgend Farbmodelle: Verschiedene Arten der Repräsentation der Farbe
    
    ![截屏2023-06-14 17.40.29.png](5_Repra%CC%88sentation%20von%20Farbe/%25E6%2588%25AA%25E5%25B1%258F2023-06-14_17.40.29.png)
    
    > **Farbkanäle**
    > 
    > 
    > Grauwert → Nur 1 Farbkanal: I
    > 
    > RGB → 3 Farbkanäle: r, g, b
    > 

# 5.3 Farbmodelle/Farbräume und Konvertierung

- **RGB (Rot, Grün, Blau)**
  
    ![Untitled](5_Repra%CC%88sentation%20von%20Farbe/Untitled%203.png)
    
- **HSI‐Farbraum (Hue, Saturation, Intensity)**
  
    > **Hue, Saturation, Intensity (色相，饱和度，亮度/强度)**
    > 
    
    ![Untitled](5_Repra%CC%88sentation%20von%20Farbe/Untitled%204.png)
    
    [HSL和HSV色彩空间 - 维基百科，自由的百科全书](https://zh.wikipedia.org/zh-cn/HSL和HSV色彩空间)
    
    Umrechnung von RGB in HSI‐Farbraum (Vorbedingung: RGB‐Werte sind auf den Bereich [0, 1] normiert):
    
    Farbwert (Hue):
    
    $$
    H =
    \left\{
    \begin{aligned}
    &\Theta \\
    &360^\circ - \Theta
    \end{aligned}
    \right.
    \begin{aligned}
    &: B \le G \\
    &: B>G
    \end{aligned} \text{\quad mit \quad}
    \Theta = \cos^{-1}
    \bigg\{
    \frac{\frac{1}{2}[(R-G)+(R-B)]}{\sqrt{[(R-G)^2+(R-B)(G-B)]}}
    \bigg\}
    $$
    
    Sättigung (Saturation):
    
    $$
    S=1-\frac{3}{(R+G+B)} \min(R+G+B)
    $$
    
    Intensität (Intensity):
    
    $$
    I=\frac{1}{3}(R+G+B)
    $$
    
- **L*a*b Farbsystem**
  
    [CIELAB色彩空间 - 维基百科，自由的百科全书](https://zh.wikipedia.org/zh-cn/CIELAB色彩空间)
    
    Helligkeits‐ und Farbunterschiede werden gleichförmiger wahrgenommen
    
- **Umrechnung in L*a*b**
  
    $$
    \begin{aligned}
    &L* = 116 f \bigg(\frac{Y}{Y_n}\bigg) \\
    &a^*=500\bigg[ f\bigg(\frac{X}{X_n}\bigg) - f\bigg(\frac{Y}{Y_n}\bigg) \bigg] \\
    &a^*=500\bigg[ f\bigg(\frac{X}{X_n}\bigg) - f\bigg(\frac{Y}{Y_n}\bigg) \bigg] \\
    &f(t)=
    \left\{
    \begin{aligned}
    &t^{1/3}\\
    &t/(3\delta ^2)+2\delta /3
    \end{aligned}
    \right.
    \begin{aligned}
    &\quad t>\delta ^3\\
    &\quad \text{else,}
    \end{aligned} \text{\quad mit \quad} \delta = \frac{6}{29}
    \end{aligned}
    $$
    
    $\mathrm{X_n,Y_n,Z_n}$ Normwerte für Zentrierung auf Beleuchtungsart, z.B. Lichtquelle mit ca. 6500K $\mathrm{X_n}$=x/y=0.95, $\mathrm{Y_n}$=1 und $\mathrm{Z_n}$=z/y=1.09
    
- **Weitere Farbmodelle**
  
    ![Untitled](5_Repra%CC%88sentation%20von%20Farbe/Untitled%205.png)
    

# 5.4 Weißabgleich

- „Weißes Objekt“
    - Reflektiert gesamtes sichtbares Spektrum gleichförmig
    - Wird vom Menschen unabhängig von der Farbtemperatur der Beleuchtung nach Adaption als „weiß“ empfunden: „Chromatische Adaption“ des Auges
- Korrektur von digitalen Bildern
    - Weißpunkt muss bekannt sein oder bestimmt werden (Pixel am Weißpunkt mit Farben r, g, b soll dem Betrachter als „weiß“ erscheinen. Z.B. hellster Punkt im Bild oder manuell gewählter Punkt)
    - Korrektur der Farben r, g, b z.B. über lineare Faktoren kR , kG , kB r‘=kRr, g‘=kGg, b‘=kBb, z.B. r‘=g‘=b‘ oder gewählt entsprechend Zielfarbtemperatur

## Zusammenfassung

5.1 Additive/Subtraktive Farbmischung

- Was passiert bei additiver/subtraktiver Farbmischung?
- Anwendungsbeispiele

5.2 Farbempfinden und technische Repräsentation von Farbe

- Grundprinzip des Farbempfindens, Einflussgrößen
(Beleuchtung, Reflexionseigenschaften Objekt, spektrale Empfindlichkeit)
- Technische Repräsentation, Normfarbtafel

5.3 Farbmodelle/Farbräume und Konvertierung

- Kenntnis verschiedener Farbräume, Motivation, Anwendung
- Konvertierung zwischen Farbräumen

5.4 Weißabgleich

- Grundprinzip, praktische Durchführung