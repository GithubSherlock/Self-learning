# 6_Einführung Bildanalyse

Created: July 15, 2023 10:53 PM

# 6_Einführung Bildanalyse

# 6.1 Einführung Bildanalyse

**Ziel der technischen Bildanalyse**:

- **Aufgabenorientierte** Interpretation des Bildinhaltes

**Problem**

- Aufgaben der Bildanalyse sind verschieden
- Lösungswege sind unterschiedlich
- Keine einheitliche Theorie

# 6.2 Diskrete Geometrie und Analyse von Binärbildern

## 6.2.1 Binäre Objekte

### 6.2.1.1 Binärbild

- Segmentierung des Bildes, z.B. durch Schwellwertbildung
  
    $$
    b(x,y)=
    \left\{
    \begin{align*}
    1:& |g(x,y)| > s\\
    0:& sonst
    \end{align*}
    \right.
    $$
    
- Binärbild: Pixelwerte können nur zwei Zustände annehmen: $p(x,y) \in \{0,1\}$
- Aufteilung der Menge der Pixel P eines Bildes in zwei Mengen $P_A$ und $\overline{P_A}$
  
    $$
    P = P_A + \overline{P_A}
    $$
    
    - $P_A$: Vordergrundpixel, 'interessante Pixel', später Objektpixel
    - $\overline{P_A}$: Hintergrundpixel, 'uninteressante Pixel

### 6.2.1.2 Nachbarschaft und Zusammenhang von Pixeln

- **Beziehungen zwischen Regionen**
    
    - Komplement (not)
    - Vereinigung (or)
    - Querschnitt (and)
    - Differenz
    - enthält
    - verschieden
    
    ![Untitled](6_Einfu%CC%88hrung%20Bildanalyse/Untitled.png)
    
- **Nachbarschaft, Zusammenhang und binäres Objekt**
    - 4er, 8er Nachbarschaften
        - 4er: $\begin{matrix}
        0&1&0\\
        1&1&1\\
        0&1&0\\
        \end{matrix}$
        - 8er: 
        $\begin{matrix}
        1&1&1\\
        1&1&1\\
        1&1&1\\
        \end{matrix}$
    - Die Nachbarschaftsrelation ist binär und symmetrisch.
    ****
- **Zusammenhang zwischen zwei Pixeln (Connection)**
    - $P_A$: Menge der Vordergrund- oder Objektpixel des Binärbildes

### 6.2.1.3 Definition binäres Objekt

- **Binäres Objekt**
    - Eine Teilmenge von Pixeln $Q_A\in P_A$ ist ein binaeres Objekt, wenn alle Pixel $q\in Q_A$ zusammenhaengend sind.
- **Zusammenhang von Regionen**
    - Mit N4 und N8 gibt es unterschiedlichen Loesungen
    
    ![Untitled](6_Einfu%CC%88hrung%20Bildanalyse/Untitled%201.png)
    
- **Klassifikation von Bildpunkten**
    - Einzelpunkt
    - Randpunkt
    - Innenpunkt
    - Bogenpunkt
- **Nachbarschaftsverfahren**
    - Algorithmen zur Bestimmung von binären Objekten aus binären Bildern

### 6.2.1.4 Zusammenhangsanalyse

- **Zusammenhangsanalyse (Connected Components)**
  
    ![截屏2023-07-16 18.02.48.png](6_Einfu%CC%88hrung%20Bildanalyse/%25E6%2588%25AA%25E5%25B1%258F2023-07-16_18.02.48.png)
    
    > Note:
    遍历整个label图像，锚点为 x, y, 分别储存upper和left的label，和 x, y 处的Binaer值 I(x,y)，当 I(x,y) 不为0的时候，分四种情况，来判断锚点处的label应该如何处理，比较特殊的第四种情况，当上和左的值一致的时候，锚点处的label直接赋予与左和上一样的值，当左侧的值和上侧的值不一样的时候，需要判断两者中最小的那个值作为锚点处的label值，并且将所有具有相对大的label值的位置上的值，更新为那个最小的值。
    > 

### 6.2.1.5 Repräsentation binärer Objekte

Binäre Objekte können im Computer als Matrix von 0en und 1en dargestellt werden, wobei 0 den Hintergrund und 1 das Objekt darstellt.

- **Beschreibung durch Richtungscodes**
    - Kettencode (Richtungscode)
    - Differentieller Kettencode (Richtungsänderungscode)
    ****
    
    ![Untitled](6_Einfu%CC%88hrung%20Bildanalyse/Untitled%202.png)
    
- **Bildpräsentation durch einen Quaternärbaum (Quadtree)**
  
    ![Untitled](6_Einfu%CC%88hrung%20Bildanalyse/Untitled%203.png)
    

## 6.2.2 Morphologische Operationen

- Motivation
    - Veränderung Formmerkmale (z.B. Glätten von Objekträndern, ...)
    - Beseitigung Störungen
    - Suche nach Formen
- **Eigenschaften von Erosion und Dilatation**
    - Verschiebungsinvarianz
      
        $$
        B \oplus S(A) = S(B \oplus A)\\
        B \ominus S(A) = S(B \ominus A)
        $$
        
    - Kommutativität
      
        $$
        B \oplus A = A \oplus B\\
        B \ominus A \ne A \ominus B
        $$
        
    - Assoziativität
      
        $$
        (B \oplus A_1) \oplus A_2 = B \oplus (A_1 \oplus A_2) = (B \oplus A_2) \oplus A_1 \\
        (B \ominus A_1) \ominus A_2 = B \ominus(A_1 \ominus A_2) = (B \ominus A_2) \ominus A_1
        $$
        
    - Dualität
      
        $$
        \overline{A\ominus B}=\overline{A}\oplus\hat{B} \\
        \overline{A\oplus B}=\overline{A}\ominus\hat{B}
        $$
    
- **Opening**
    - Kombination von Erosion gefolgt von einer Dilatation
    - Entfernung aller (Teil)strukturen, die kleiner als das Strukturelement sind
    - Kontur bleibt fast unverändert wird
- **Closing**
    - Kombination von Dilatation gefolgt von einer Erosion
    - Schließen von kleinen Löchern
    - Wiederherstellung der ursprünglichen Größe des Objekts
- **Hit or Miss Operatoren**
    - einzelner Pixel: $\begin{matrix}
    0&0&0\\
    0&1&0\\
    0&0&0\\
    \end{matrix}$
    - untere rechte Ecken: $\begin{matrix}
    x&1&0\\
    1&1&0\\
    0&0&0\\
    \end{matrix}$
    - Randpunkte von oben: $\begin{matrix}
    0&0&0\\
    x&1&x\\
    1&1&1\\
    \end{matrix}$
- Morphologische Operationen auf Grauwertbildern
    - Erosion (min)
        - Effekt: Dunkle Bereiche werden vergrößert, deutlich sichtbar
    - Dilatation (max)
        - Effekt: Helle Bereiche werden vergrößert, deutlich sichtbar
    - Opening: Kombination von Erosion gefolgt von einer Dilatation
        - Erosion
        Entfernung aller (Teil)strukturen, die kleiner als das Strukturelement sind
        - Dilatation
        Wiederherstellung der *ursprünglichen Größe* des Objekts mit Ausnahme der
        vollständig entfernten Teilstrukturen
    - Closing: Kombination von Dilatation gefolgt von einer Erosion
        - Dilatation
        Schließen von kleinen Löchern (kleiner als das Strukturelement)
        - Erosion
        Wiederherstellung der *ursprünglichen Größe* des Objekts

## 6.2.3 Distanzen und Distanztransformation

- **Abstand in diskreten Gittern**
    - Euklidischer Abstand
        - $d_e[(i,j),(h,k)]=\sqrt{(i-h)^2+(j-k)^2}$
    - City-Block-Abstand
        - $d_4[(i,j),(h,k)]=|i-h|+|j-k|$
    - Schachbrettabstand
        - $d_8[(i,j),(h,k)]=\max(|i-h|,|j-k|)$
- **Distanztransformation**
    - Ablauf
        1. Erosion des Bildes $I_k = I_{k-1}\ominus B$
        2. Rand der Iterationsstufe k ist $R_k=I_{k-1}-I_k$
        3. Pixel des Randes $R_k$ werden mit Distanz *k* im Distanzbild bespeichert
    - Beispiel:
      
        ![Untitled](6_Einfu%CC%88hrung%20Bildanalyse/Untitled%204.png)
    
- Besonderheiten der Distanztransformation
    - sehr empfindlich auf Störungen
    - häufig vorherige Glättungen im Binärbild
- Anwendung
    - Objekterkennung
        - Objektmodell
            - Binäres Template
        - Matching
            - Vergleich Template **nicht** direkt mit Bilder, sondern
            - Konturdetektion im Bild
            - Distanzkarte von Konturbild
            - Vergleich Template mit Distanzkarte
            
            ![截屏2023-07-17 00.27.03.png](6_Einfu%CC%88hrung%20Bildanalyse/%25E6%2588%25AA%25E5%25B1%258F2023-07-17_00.27.03.png)
    
- **Medial-Achsen-Transformation (MAT) oder Skelettierung**
    - Skelett eines digitalen Objektes
    - Skelettpunkte, sind die Zentren der maximalen eingeschriebenen Kreise
    - Vorgehen
        - Distanztransformation
        - Suche lokaler Maxima entsprechend gewaehlter Nachbarschaft

## 6.2.4 Eigenschaften binärer Objekte

- Motivation
    - Berechnung von Merkmalen für eine Klassifikation
- Merkmale für Binärobjekte
    - Fläche A
    - Umfang U
    - Länge L
    - Breite W
    - Formfaktor f
        - $f = \frac{U^2}{4\pi A}$ mit Kreis: f = 1, sonst f > 1
- **Momente**
    - Bildmomente
      
        $$
        m_{pq}=\sum^{M}_{x=1}\sum^{N}_{y=1}B(x,y)x^py^q
        $$
        
        - Fläche
    - Zentralmomente
      
        $$
        \mu_{pq}=\sum^{M}_{x=1}\sum^{N}_{y=1}B(x,y)(x-x_s)^p (y-y_s)^q
        $$
        
        - z.B. für Berechnung Trägheitsmomente, Formmerkmale
    - mit den Schwerpunktskoordinaten
      
        $$
        x_s= \frac{m_{10}}{m_{00}} \text{ und } y_s= \frac{m_{01}}{m_{00}}
        $$
        
        - Berechnung Schwerpunkt des Binärobjektes
- Moment Tensor
    - $J$
    - $\theta$

## Zusammenfassung

- Nachbarschaft, Zusammenhang, binäre Objekte
- Connected Components Verfahren
- Repräsentation binärer Objekte (Labelbild, Richtungscodes, Quadtree)
- Morphologische Operatoren, Strukturierendes Element
- Erosion, Dilatation, Opening, Closing
- Distanzen und Distanztransformation, Medial-Axis-Transformation
- Berechnung Merkmale digitaler Objekte

# 6.3 Bildsegmentierung

<aside>
💡 **Was ist die ideale Segmentierung?**

Die ideale Segmentierung ist eine, die die relevanten Objekte in einem Bild genau trennt, ohne Übersegmentierung oder Untersegmentierung zu verursachen. Die ideale Segmentierung sollte auch robust gegenüber Rauschen und Beleuchtungsvariationen sein und das gesamte Objekt mit klaren Grenzen erfassen.

</aside>

- Segmentierung
    - Vorverarbeitungsschritt für die weitere Bildanalyse
    - Jedes Pixel wird einem Segment zugeordnet
    - Pixel innerhalb eines Segment sind zusammenhängend
    - Zusammenhängende Pixel eines Segmentes haben eine gleiche Bedeutung
- Types of segmentation
    - Oversegmentation
    - Undersegmentation
    - Multiple Segmentations

![Untitled](6_Einfu%CC%88hrung%20Bildanalyse/Untitled%205.png)

## 6.3.1 Schwellwertverfahren (Pxielbasiert)

$$
b(x,y)=\left\{
\begin{aligned}
&1 : g(x,y)>s\\
&0 : sonst
\end{aligned}
\right.
$$

- Schwellenwertverfahren
    - Voraussetzung
        - Die Grauwerte des gesuchten Objekts unterscheiden sich signifikant von denen des Hintergrunds
- Schwellwertbestimmung
    - Manuell
    - Automatisch
        - Analyse des Grauwerthistogrammes mit der Annahme von zwei Gaussverteilungen:
            - Verteilung1: Von Links nach Rechts
            - Verteilung2: Von Rechts nach Links
        - Verfahren nach Otsu
            - Suche einer Schwelle **s**, so dass Varianz zwischen den Klassen möglichst gross und Varianz innerhalb der Klassen möglichst klein.
            - Berechnung Quotient Q(s) aus Varianz $\sigma^2_{zw}$ den Klassen und Varianz $\sigma^2_{in}$ in den Klassen.
- Ungleichförmige Beleuchtung oder Hintergruende
- Globale Schwellen
    - Globale Schwellen fuehren zu ungleichmäßiger Segmentierung
- Ortsvarianten Histogrammen
    - Lokale Histgramme
    - Lokale Schwellwerte
- Zusammenfassung Schwellwertverfahren
    - Einfache Segmentierung
    - Anwendung
        - Industrielle Bildverarbeitung
        - Medizinische Bildverarbeitung
    - Manuelle oder automatische Bestimmung der Schwellwerte
    - Umgang mit ungleichförmiger Beleuchtung

## 6.3.2 Flächenbasierte Segmentierung (Region‐Growing, Split and Merge)

- **Regionenbasierte Segmentierung**
    - **Homogenität** im Inneren des Segments
    - Homogenitätsbedingung wird **bei der Segmentierung** ausgewertet
    - Homogenität ist **relativ** zu den Attributen eines Segments definiert

<aside>
💡 **Was zeichnet eine homogene Region aus?**

Mögliche Homogenitätskriterien

- Gleicher Grauwert
- Gleiche Farbe
- Gleiche Varianz der Grauwerte
- Gleiche Texturmerkmale
- Gleiche Bewegungsvektoren (Bildfolge)
</aside>

<aside>
💡 **Wie finde ich homogene Regionen?**

Zwei einfache Algorithmen zum Finden homogener Regionen:

- Region Growing
- Split and Merge Verfahren
</aside>

- **Region Growing (Regionen Suche)**
    - Grundidee des Algorithmus:
        - Auswahl von Startpixeln („Saatpixel"), die bisher keinem Segment zugeordnet wurden
        - Schrittweise Erweiterung der Segmente um einzelne benachbarte Pixel
        - Neu zum Segment hinzugefügte Pixel müssen ein Homogenitätskriterium des Segments erfüllen (z.B. Differenz zum mittleren Grauwert)
    
    ![Untitled](6_Einfu%CC%88hrung%20Bildanalyse/Untitled%206.png)
    
    - Prüfung des Homogenitätskriteriums: $h(p_n,p_r)<T$
    - Entscheidungsmethoden
        - Differenz zum Nachbarpixel
        - Differenz zum Startpixel
            - Interaktiv
            - Hellste Pixel
            - Dunkelste Pixel
        - Differenz zum mittleren Pixel
        - Differenz zu Umgebungspixeln
    - Vorteile
        - Einfache Implementierung
        - Begrenzter Rechenaufwand
    - Nachteile
        - Bildmaterial muss für Algorithmus geeignet sein
            - Geeignete Textur der Regionen
            - Definierte Beleuchtungsbedingungen
        - Anpassung des Schwellwertes häufig kritisch
- **Split‐ and Merge Verfahren**
  
    <aside>
    💡 **Unterschiede zwischen Region Growing und Split‐ and Merge Verfahren?**
    
    - Region Growing
        - „Saatpixel“
        - Erweiterung homogener Bereiche
    - Split‐ and Merge Verfahren
        - Aufteilung (split) inhomogener Bereiche in einer Quadtree‐Struktur
        - Zusammenführen (merge) homogener Teilbereiche
        </aside>
    
    ![Untitled](6_Einfu%CC%88hrung%20Bildanalyse/Untitled%207.png)
    
    - Vorteile
        - Einfache Implementierung
        - Begrenzter Rechenaufwand
    - Nachteile
        - Bildmaterial muss für Algorithmus geeignet sein
            - geeignete Textur der Regionen
            - definierte Beleuchtungsbedingungen
        - Anpassung des Schwellwertes häufig kritisch
- Watersheidentransformation **(nicht Klausur relevant)**
    - Vorteile
        - Einfache zu implementieren
        - Erfordert weinig Rechenleistung
    - Nachteile
        - Nur fuer geeignetes Bildmaterial sinnvoll
        - Richtige Wahl des Schwellwertes

## 6.3.3 Kantenfindung, Canny‐Edge

- **Canny Edge**
  
    [Canny边缘检测算法](https://zhuanlan.zhihu.com/p/42122107)
    
    - Anforderungen an einen Detektor
        - – **Güte der Detektion:** Detektion möglichst aller relevanten Kanten
        - – **Genaue Lokalisation:** Detektierte Kanten sollen möglichst dicht an den Kanten im Grauwertbild liegen
        - – **Eindeutige Detektion:** Eine reale Kante sollte möglichst nur einmal detektiert werden, d.h. keine Mehrfachdetektionen bei verrauschten Kanten; detektierte Kante 1 Pixel breit
    - Rauschunterdrückung
        - Gaussfilter
    - Kantendetektion
        - Sobel
            - Kantenstärke: $G=\sqrt{G_x^2+G_y^2}$
            - Kantenrichtung: $\theta = \arctan(\frac{G_y}{G_x})$
            - Quantisierung der Kantenrichtungen: $\Theta_Q = \{0\degree,45\degree,90\degree,135\degree\}$
        - Roberts
        - Prewitt
    - Algorithmus
        - Einteilung der Pixel in 3 Kategorien (entsprechend Ihrer Kantenstärke)
          
            ![截屏2023-07-17 16.51.33.png](6_Einfu%CC%88hrung%20Bildanalyse/%25E6%2588%25AA%25E5%25B1%258F2023-07-17_16.51.33.png)
            
        - Klassifikation der Pixel in Kanten und „nicht Kanten“ Pixel
            - 'strong pixel' - Kantenpixel, z.B. K (x,y) := 1
            - 'weak pixel' - keine Kantenpixel, K (x,y) := 0
            - 'candidate pixel - Verfolgung der Pixel im Bild G entlang beider Kantenrichtungen, so lange G(x,y) 'Candidate'
              Wenn entstehende Kette der Pixel mit einem 'strong' Pixel verbunden ist
                - dann sind alle Pixel der Kette ein Kantenpixel K(x,y) := 1
                - sonst sind alle Pixel der Kette kein Kantenpixel K(x,y) := 0
- **Zusammenfassung Canny‐Edge Detector**
    - Einfaches, robustes Verfahren zur Detektion von Kanten im Bild
    - Adaption von zwei Schwellwerten $(T_{low},T_{high})$ erforderlich
    - Algorithmus
        1. Rauschunterdrückung (Glättungsfilter)
        2. Berechnung Gradientenstärke, Gradientenrichtung
        3. Unterdrückung Non Maxima
        4. Kantenverfolgung mit „Hysterese"-Schwellwert
    - Auch Teile des Canny‐Algorithmus findet man häufig in Anwendungen zur Kantendetektion

## Zusammenfassung-Bildsegmentierung

- Bildsegmentierung
    - Vorverarbeitungsschritt für die weitere Bildanalyse
    - Annahme: Segmente im Bild, d.h. zusammengehörende Pixel, haben eine einheitliche Bedeutung im Sinne einer späteren Bildinterpretation
    - Pixel eines Segmentes sind durch ähnliche Eigenschaften der Pixel, bzw. Pixelumgebung charakterisiert
    - Jedes Pixel kann in der Regel nur einem Segment zugehören
- Die Segmentierung des Bildes anhand von pixelbezogenen Eigenschaften wird als datengetrieben Bildsegmentierung bezeichnet.
- Weiterverarbeitung (z.B. Klassifikation der Bildsegmente)
    - Binärbildverarbeitung
- Größe der Segmente
    - Form
    - Farbe
    - Textureigenschaften
    - …

# 6.4 Template‐Matching und Korrelation

- **Ziel**
    - Template finden
- Vorgehen
    - Platziere Template an allen Positionen (x,y) im Bild (systematische Suche)
    - Berechne Unterschied zwischen Template und zugehörigem Bildausschnitt („Patch“)
    
    $$
    d(x,y) = d[g,f]
    $$
    

<aside>
💡 **Was ist ein gutes Distanzmaß um die Ähnlichkeit von zwei Patches zu messen?**

- Correlation
  
    $$
    h[m,n] = \sum_{k,l}g[k,l]f[m+k,n+l]
    $$
    
- Zero‐Mean Correlation
  
    $$
    h[m,n] = \sum_{k,l}(g[k,l]-\overline{g})(f[m+k,n+l])
    $$
    
- Sum of Squared Differences
  
    $$
    h[m,n] = \sum_{k,l}(g[k,l]-f[m+k,n+l])^2
    $$
    
- Normalized Cross Correlation
  
    $$
    h[m,n] = \frac{\sum_{k,l}(g[k,l]-\overline{g})(f[m+k,n+l]-\overline{f}_{m,n})}{\left(\sum_{k,l}(g[k,l]-\overline{g})^2\sum_{k,l}(f[m+k,n+l]-\overline{f}_{m,n})^2\right)^{0.5}}
    $$
    

</aside>

- Betrachtung Rechenaufwand
    - vollständige Suche ueber alle Bildpositionen
    - Annahme Bildgroesse N, M und Templategroesse K, L und SAD N*M*K*L - Differenzberechnungen
- **Template Matching und geometrische Transformationen**
    - Bisher vorgestelltes Verfahren modelliert nur Translation (2 Parameter) ****zwischen Template und Objekt im Bild
    - Erweiterung auf Rotation und Skalierung möglich
    - Aber ****starke Erhöhung des Rechenaufwandes
- **Anwendungen Template Matching**
    1. Bewegungsschätzung in Bildkodierung (‚Blockmatching‘)
    2. Detection: Shape‐based Matching
    3. Klassifikation

# 6.5 Suche geometrischer Primitive (Hough)

- Motivation
    - Globale Suche nach geometrischen Primitiven
        - Geraden
        - Kreisen
        - Beliebig geformten Konturen (verallgemeinerte Hough-Transformation)
    - Robust gegenüber Unterbrechungen der Kanten, ...
- **Hough‐Transformation für Geraden**
  
    $$
    y=ax+b \\
    d=\cos{\phi}\cdot x+\sin{\phi}\cdot y
    $$
    
- **Algorithmus Hough‐Transformation für Geraden**
    1. Bereitstellung eines „Akkumulators“: d, φ - Raum → Hough‐Raum
    2. Für jeden Kantenpunkt (x,y) im Bild für φ = -90° bis 90°
        - Berechne d=cos(φ)*x+sin(φ)*y
        - Akkumuliere: Hough-Raum(d,φ)++;
    3. Suche Maxima im Hough‐Raum als Geraden im Bild
- **Effekte der Quantisierung**
    - Die Parameter einer Linie können mit einer feineren Quantisierung genauer bestimmt werden
    - Feinere Quantisierung erhöht Rechenzeit und Speicherbedarf
    - Für Toleranz gegenüber Rauschen ist eine gröbere Quantisierung besser
- **Erweiterung der Hough Transformation für Kreis**
  
    $$
    (x-x_0)^2+(y-y_0)^2=r^2
    $$
    
    - Ein Kreis hat drei Parameter: $(x_0,y_0),r$
    - Voting für jedes Pixel: je eine Linie im Parameterspace
    - Sehr hoch Rechenaufwand
- **Verallgemeinerung für beliebige analytische Kurven**
    - Implizite Funktion: $f(x,y,a)=0$
    - Normale n auf Funktion
    - Berechne alle (x, y, **a**) für die beide obige Gleichungen erfüllt sind und inkrementiere einen Akkumulator
      
        $$
        f(x,y,a)=f(x,y,a)+1
        $$
        

## Zusammenfassung

- Einführung Hough‐Transformation für Linien: Parameter‐space, Voting
- Erweiterung auf Kreise
- Nutzung der Gradientenrichtung
- Verallgemeinerung für beliebige analytische Kurven
- Verallgemeinerte Hough‐Transformation (R‐Table, ….)