# 4_Signalorientierte Bildverarbeitung

Created: July 13, 2023 3:14 PM

# 4_Signalorientierte Bildverarbeitung

![4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-12_23.08.01.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-12_23.08.01.png)

Motivation für eine Repräsentation des Bildes und von Bildoperationen in einem „Transformationsbereich“

- Hilfsmittel für die Modellierung von Signal‐ oder Systemverhalten und entstehende Veränderungen in Bildern
- Beschreibung der Eigenschaften von Filtern
- Bildrestauration, Invertierung von Störungen
- Nutzung von Transformationskoeffizienten für die Datenkompression
- Berechnung von Merkmalen für die Segmentierung und Klassifikation von Bildinhalten

# 4.1 Das Bild als Signal

### Begriffe

- kontinuierliches Signal
- zeit bzw. ortsdiskretes Signal
- periodisches Signal
- mehrdimensionales Signal

---

![4_Signalorientierte%20Bildverarbeitung/Untitled.png](4_Signalorientierte%20Bildverarbeitung/Untitled.png)

### Bildmodelle

---

![4_Signalorientierte%20Bildverarbeitung/Untitled%201.png](4_Signalorientierte%20Bildverarbeitung/Untitled%201.png)

# 4.2 Grundlagen unitäre Transformation

## 1D Fourier‐Transformation

Motivation:

- Beschreibung Signal/Systeme im „Frequenzraum“
- Hilfsmittel für bessere Erklärbarkeit von Signal‐ oder Systemeigenschaften

### Annäherung von mathematischer Seite

- **Linearer Raum/Vektorraum**
- **Lineare Unabhängigkeit von Vektoren/Basis**
    - Es sei E ein linearer Raum.
      Es sind $\mathrm{x_1,\dots,x_n \in E}$ Vektoren in $\mathrm{E}$ und $\mathrm{\lambda_1,\dots,\lambda_n \in K}$. Die Vektoren $\mathrm{x_1,\dots,x_n}$ heißen linear unabhängig, wenn
      
      $$
        \lambda_1 x_1+\lambda_2 x_2+\dots+\lambda_n x_n = 0 \Leftrightarrow \lambda_1 = \lambda_2 = \dots =\lambda_n =0
      $$
      
        Anderenfalls sind die Vektoren linear abhangig.
      

<aside>
💡 **Was ist die maximale Anzahl linear unabhängiger Vektoren?**

Dimension des Raumes

</aside>

- **Einheitsvektoren**
- **Skalarprodukt**
    - **Unitärer Raum $C^n$:** Linearer Raum über **komplexen** Zahlen mit Skalarprodukt
    - **Euklidischer Raum $R^n$:** Linearer Raum über **reellen** Zahlen mit Skalarprodukt
- **Orthogonalität**
  
    Sei E ein lineaer Raum mit Skalarprodukt. Zwei Vektoren f und g aus E heißen orthogonal, wenn <f,g>=0.
    
    $$
    \mathrm{f}=\begin{pmatrix}
    f_1\\
    f_2\\
    \vdots\\
    f_N
    \end{pmatrix} \quad
    \mathrm{g}=\begin{pmatrix}
    g_1\\
    g_2\\
    \vdots\\
    g_N
    \end{pmatrix} \quad
    f \perp g \Leftrightarrow
    \sum\limits_{i=1}^N{f_i g_i}=0
    $$
    

**Unitäre Transformation**

Ziel: Repräsentation des Bildes mittels der hier gegebene Basisvektoren
****

- Rekonstruktion
    - Ortsbereich → Transformationsbereich
- Rücktransformation
    - Transformationsbereich → Ortsbereich

> **Wie berechne eine unitäre Transformation?**
> 
> - $\mathrm{f}$ ein Vektor in einem Hilbertraum und
> - $\mathrm{(b_1,b_2,\dots,b_n)}$ eine Orthonormalbasis in diesem Raum
> 
> Verallgemeinerte Fourierreihe:
> 
> $$
> \mathrm{f}=\sum\limits_{k=1}^N<\mathrm{f},b_k>b_k=\sum\limits_{k=1}^N{F_k b_k}
> $$
> 
> Verallgemeinerte Fourierkoeffizient:
> 
> $$
> \mathrm{F}_k=<\mathrm{f, b}_k>
> $$
> 
> später verwendete Darstellung: $\mathrm{f} \Leftrightarrow \mathcal{F}$
> 
> **Beispiel:**
> 
> Gegeben ein $2 \times 2$ Bild
> 
> $$
> f_{xy} =
> \begin{bmatrix}
> 1 & 1\\
> 3 & 2
> \end{bmatrix}
> $$
> 
> Basisvektoren für unitäre Transformation:
> 
> $$
> \mathrm{
> b_0=\frac{1}{2}
> \begin{bmatrix}
> 1 & 1\\
> 1 & 1
> \end{bmatrix} \quad
> b_1=\frac{1}{2}
> \begin{bmatrix}
> -1 & -1\\
> 1 & 1
> \end{bmatrix} \quad
> b_2=\frac{1}{2}
> \begin{bmatrix}
> 1 & -1\\
> -1 & 1
> \end{bmatrix} \quad
> b_3=\frac{1}{2}
> \begin{bmatrix}
> 1 & -1\\
> 1 & -1
> \end{bmatrix} \quad
> }
> $$
> 
> Berechnung der Transtormationskoefizienten (veraligemeinerte Fourierkoetfizienten):
> 
> $$
> \left.
> \begin{aligned}
> \alpha_0
> \quad &= \quad
> \mathrm{<f_{xy},b_0>}
> \quad = \quad
> <
> \begin{bmatrix}
> 1 & 1\\
> 3 & 2
> \end{bmatrix},
> \frac{1}{2}
> \begin{bmatrix}
> 1 & 1\\
> 1 & 1
> \end{bmatrix} >
> 
> \quad = \quad
> +\frac{7}{2} \\
> \alpha_1
> \quad &= \quad
> \mathrm{<f_{xy},b_1>}
> \quad = \quad
> <
> \begin{bmatrix}
> 1 & 1\\
> 3 & 2
> \end{bmatrix},
> \frac{1}{2}
> \begin{bmatrix}
> -1 & -1\\
> 1 & 1
> \end{bmatrix} >
> 
> \quad = \quad
> +\frac{3}{2} \\
> \alpha_2
> \quad &= \quad
> \mathrm{<f_{xy},b_2>}
> \quad = \quad
> <
> \begin{bmatrix}
> 1 & 1\\
> 3 & 2
> \end{bmatrix},
> \frac{1}{2}
> \begin{bmatrix}
> 1 & -1\\
> -1 & 1
> \end{bmatrix} >
> 
> \quad = \quad
> -\frac{1}{2} \\
> \alpha_3
> \quad &= \quad
> \mathrm{<f_{xy},b_3>}
> \quad = \quad
> <
> \begin{bmatrix}
> 1 & 1\\
> 3 & 2
> \end{bmatrix},
> \frac{1}{2}
> \begin{bmatrix}
> 1 & -1\\
> 1 & -1
> \end{bmatrix} >
> 
> \quad = \quad
> +\frac{1}{2}
> \end{aligned}
> \right.
> $$
> 
> Rekonstruktion des Bildes oder Ruecktransformation:
> 
> $$
> \left.
> \begin{aligned}
> \mathrm{f_{xy}} &= \sum\limits_{i=0}^3{\alpha_i\cdot \mathrm{b_i}}\\
> &=
> \frac{7}{2}\frac{1}{2}
> \begin{bmatrix}
> +1 & +1\\
> +1 & +1
> \end{bmatrix}
> \quad + \quad
> \frac{3}{2}\frac{1}{2}
> \begin{bmatrix}
> -1 & -1\\
> +1 & +1
> \end{bmatrix}
> \quad + \quad
> -\frac{1}{2}\frac{1}{2}
> \begin{bmatrix}
> 1 & -1\\
> -1 & 1
> \end{bmatrix}
> \quad + \quad
> \frac{1}{2}\frac{1}{2}
> \begin{bmatrix}
> 1 & -1\\
> 1 & -1
> \end{bmatrix} \\
> &=
> \frac{1}{4}
> \begin{bmatrix}
> +4 & +4\\
> +12 & +8
> \end{bmatrix} =
> \begin{bmatrix}
> 1 & 1\\
> 3 & 2
> \end{bmatrix}
> \end{aligned}
> \right.
> $$
> 
> Ortsbereich ↔ Transformationsbereich:
> 
> $$
> \mathrm{f_{xy}} =
> \begin{bmatrix}
> +1 & +1\\
> +3 & +2
> \end{bmatrix}
> \Leftrightarrow
> \frac{1}{2}
> \begin{bmatrix}
> +7 & +3 & -1 & +1
> \end{bmatrix}
> $$
> 

## Zusammenfassung

- Linearer Raum, Orthonormalbasis, Skalarprodukt
- Unitäre Transformation
- Repräsentation eines Bildes als Linearkombination von Basisvektoren
→ Repräsentation des Bildes im „Transformationsbereich”

Beispiele für Bildverarbeitung:

- (Diskrete) Fourier-Transformation (DFT)
- Diskrete Kosinus Transformation (DCT)
- Hadamard-Transformation
- Haar-Transformation
- Wavelet-Transformation

# 4.3 Fourier‐Transformation

### Fourierreihe für periodische Funktionen

### 1D Diskrete Fourier‐Transformation

**Fourierreihe und Fourierkoeffizienten:**

$$
f(t) \quad = \quad \frac{1}{\sqrt{T}} \sum_{k=-\infty}^{\infty} F_k e^{j2\pi k \frac{t}{T}} ;
\quad \Leftrightarrow \quad
F_k=\frac{1}{\sqrt{T}} \int_0^T f(t) e^{-j2\pi k \frac{t}{T}} dt
, \quad ±k=0,1,2,3,\cdots
$$

Eulersche Formel: $\mathrm{e^{jt}}=\cos(t) + \mathrm{j}\sin(t)$

- Frequenz-Spektrum: $\{F_k\}$
- Amplituden-Spektrum: $\{
|F_k|=\sqrt{Re(F_k)^2+Im(F_k)^2}
\}$
- Leistungs-Spektrum: $\{F_k^2\}$
- Phasenspektrum: $\phi_k=\{\arctan\frac{Im(F_k)}{Re(F_k)}\}$

![4_Signalorientierte%20Bildverarbeitung/Untitled%202.png](4_Signalorientierte%20Bildverarbeitung/Untitled%202.png)

**Fourier‐Transformation ausgewählter Funktionen**

![4_Signalorientierte%20Bildverarbeitung/Untitled%203.png](4_Signalorientierte%20Bildverarbeitung/Untitled%203.png)

### 2D Diskrete Fourier‐Transformation (DFT)

Bild als Matrix f(x, y) über linearem Raum $\mathrm{E}=R_{N \times M}$.

Skalarprodukt (jetzt Summierung iiber 2 Dimensionen):

$$
<f,g>=
\sum\limits_{x=0}^{N-1}
\sum\limits_{y=0}^{M-1}
f(x,y)\overline{g(x,y)}
$$

Basisfunktionen:

$$
\mathrm{b}_{i,k}(x,y)=
\frac{1}{\sqrt{N}}\frac{1}{\sqrt{M}} e^{j2\pi k \frac{x}{N}}
e^{j2\pi k \frac{y}{M}}
$$

DFT:

$$
⁍
$$

Inverse DFT:

$$
f(x,y) = \frac{1}{\sqrt{N}}\frac{1}{\sqrt{M}} \sum_{i=0}^{N-1}\sum_{i=0}^{M-1} F_{i,k} e^{j2\pi k \frac{x}{N}}
e^{j2\pi k \frac{y}{M}}
$$

![4_Signalorientierte%20Bildverarbeitung/Untitled%204.png](4_Signalorientierte%20Bildverarbeitung/Untitled%204.png)

Hinweis: F(0,0) in Bildmitte verschoben Interpretation: niedrige, hohe Frequenzen

mit Störung:

![4_Signalorientierte%20Bildverarbeitung/Untitled%205.png](4_Signalorientierte%20Bildverarbeitung/Untitled%205.png)

![4_Signalorientierte%20Bildverarbeitung/Untitled%206.png](4_Signalorientierte%20Bildverarbeitung/Untitled%206.png)

![4_Signalorientierte%20Bildverarbeitung/Untitled%207.png](4_Signalorientierte%20Bildverarbeitung/Untitled%207.png)

**Bedeutung von Amplitude und Phase**

![4_Signalorientierte%20Bildverarbeitung/Untitled%208.png](4_Signalorientierte%20Bildverarbeitung/Untitled%208.png)

### Eigenschaften der Fourier‐Transformation

- **Separierung der DFT**
  
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%209.png](4_Signalorientierte%20Bildverarbeitung/Untitled%209.png)
    
- **Linearität**
  
    $$
    F[a \cdot f(t)+b \cdot g(t)]
    =
    aF[f(t)]+bF[g(t)]
    $$
    
- **Parsevalsche Gleichung**
  
    $$
    \sum_k{F_k^2}=\sum_i{f_i^2}
    $$
    
- **Periodizität der DFT**
  
    Periodizitat der Basisfunktionen der diskreten Fouriertransformation:
    
    $$
    e^{-j\frac{2\pi i}{N}} =
    e^{-j\frac{2\pi (i+nN)}{N}}; \quad
    e^{-j\frac{2\pi i}{N}\frac{2\pi k}{M}} =
    e^{-j\frac{2\pi (i+nN)}{N}\frac{2\pi (k+mM)}{M}};
    $$
    
    Periodizitat des Signales im Zeit- bzw. Ortsbereich:
    
    $$
    f(i)=f(i+n\cdot N);\quad
    f(x,y)=f(x+n\cdot N,y+m\cdot M)
    $$
    
    Periodizität der Fourierkoeffizienten:
    
    $$
    F(i)=F(i+n\cdot N);\quad
    F(x,y)=F(x+n\cdot N,y+m\cdot M)
    $$
    
    Bildmodell: Bild als periodische Funktion
    
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2010.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2010.png)
    
- **Symmetrieeigenschaften der DFT**
  
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2011.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2011.png)
    

## Zusammenfassung

Fourier-Transformation

- 1D: Fourierreihe / Diskrete Fourier-Transformation (DFT)
- 2D: Diskrete Fourier-Transformation (DFT)
- Eigenschaften der Fourier-Transformation
- Fourier-Transformation nachfolgend als Hilfsmittel für Beschreibung von Filtern und Systemen

Statistische Eigenschaften von natürlichen Bildern:

- Zumeist ist Hauptanteil der Energie in niedrigen Frequenzen

# 4.4 LSI‐Systeme, Faltung und Fourier‐Transformation

### Diskretes System

- **LTI‐System** (Linear‐Time‐Invariant), **LSI‐System** (Linear‐Shift‐Invariant)
- LTI‐System durch Faltungsoperation beschreibbar
    - Faltung: h(n) = g(n)*f(n)
- Bestimmung Systemfunktion aus Impulsantwort:
    - Impulsantwort: f(n) = f(n)*δ(n)

### Linear Time/Shift Invariant System

- Ein System bildet eine Eingangsfolge g(n) auf eine Ausgangsfolge h(n) ab
g(n) → T(g(n)) → h(n)
- Ein lineares, verschiebungsinvariante System hat folgende Eigenschaften:
    - Linearität
      
        $$
        T[a_1 g_1(n)+a_2 g_2(n)] = a_1T[g_1(n)]+ a_2T[g_2(n)]
        $$
        
    - Verschiebungsinvarianz (Shiftinvarianz)
      
        $$
        T[g(n-n_0)]i = T[g(n)]{i-n_0}
        $$
        

### Faltungsoperation

- Kommutativität

$$
f * g = g * f
$$

- Assoziativität

$$
f * (g * h) = (f * g) * h
$$

### Faltung und Fourier‐Transformation

$$
FT[f*g]_l=FT[f]_l\cdot FT[g]_l
$$

![4_Signalorientierte%20Bildverarbeitung/Untitled%2012.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2012.png)

### Beschreibung und Modellierung von Systemen

Faltung in Ortsraum und Zeitraum ist die Multiplikation in Frequenzraum

**1D:**

![4_Signalorientierte%20Bildverarbeitung/Untitled%2013.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2013.png)

**2D:**

![4_Signalorientierte%20Bildverarbeitung/Untitled%2014.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2014.png)

### Filterung im Fourierraum/Frequenzbereich

![4_Signalorientierte%20Bildverarbeitung/Untitled%2015.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2015.png)

### Eigenschaften der DFT

![4_Signalorientierte%20Bildverarbeitung/Untitled%2016.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2016.png)

## **Zusammenfassung**

- Lineare Systeme → Faltungsoperation
- Zusammenhang zur Fourier‐Transformation

**Anwendung:**

- Beschreibung und Modellierung von Systemen
- Entwurf von Filtern
- Filterung im Frequenzbereich

# 4.5 Abtastung und Rekonstruktion, Abtasttheorem

### Motivation

$$
\text{Analoges Signal}\rightarrow \text{Abtastung}\rightarrow \text{Diskretes Signal}(g_d(i)) \\
\text{Rekonstruktiontes Signal} \leftarrow 
\text{Rekonstruktion} 
\leftarrow 
\text{Diskretes Signal}
(g_d(i))
$$

<aside>
💡 **What is Aliasing Problem? / Was ist Aliasing Problem?**

Definition: Aliasing ist ein Phänomen, das bei der digitalen Bildverarbeitung auftritt, wenn die Abtastrate nicht hoch genug ist, um die Details eines Signals genau zu erfassen. Es führt zu einer Verzerrung oder falschen Darstellung des Originalbildes.

Ursache: $f_{\text{sample}} \le f_{\text{Nyquist}} = 2 \cdot f_{\max}$

Lösung: Erhöhung der Abtastrate oder durch Anwendung von Anti-Aliasing-Filtern vor der Abtastung.

**Reply by ChatGPT:**

Aliasing is a phenomenon that occurs in digital image processing when the sampling rate is not high enough to accurately capture the details of a signal. It results in distortion or false representation of the original image.

In the context of digital images, aliasing occurs when the sampling rate is not sufficient to capture the high-frequency components of the image. This can happen when the image is sampled at a rate lower than the Nyquist rate, which is defined as twice the highest frequency present in the image. When the Nyquist rate is not met, high-frequency components are aliased or mapped onto lower frequencies, resulting in a distorted image.

Aliasing can be reduced by increasing the sampling rate or by applying anti-aliasing filters before sampling. Anti-aliasing filters remove high-frequency components from the signal before it is sampled, thus reducing the chance of aliasing.

</aside>

### Abtasttheorem

**1D:**

![4_Signalorientierte%20Bildverarbeitung/Untitled%2017.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2017.png)

**2D:**

![4_Signalorientierte%20Bildverarbeitung/Untitled%2018.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2018.png)

**Abtastung von Bildern**

![4_Signalorientierte%20Bildverarbeitung/Untitled%2019.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2019.png)

## Zusammenfassung

- Abtastung
- Interpretation im Frequenzbereich
- Rekonstruktion
- Abtasttheorem
- Aliasing
- Abtastratenreduktion

Wichtig für die Bildverarbeitung:

- Tiefpassfilterung vor Unterabtastung vermeidet Aliasing

# 4.6 Filterung des Bildes

### Motivation für die Filterung

a) Visuelle „Verbesserung“ von Bildern:

- Kontrast
- Rauschunterdrückung
- Schärfen
- ...

b) Vorbereitung Bildanalyse

- Detektion lokaler Strukturen: Kanten, Ecke, Linien, gleichförmige Bildbereiche
- Berechnung von Texturmerkmalen
- ...

## 4.6.1 Filter im Ortsbereich

### 4.6.1.1 **Rückblick: Klassen von Operationen**

- Punktoperation
  
    $$
    h(x,y)=F[g(x,y)]
    $$
    
- Lokale Operation
  
    $$
    h(x,y)=F[\{g(x+i,y+j);i=I_1,\cdots,I_2;j=J_1,\cdots,J_2\}]
    $$
    
- Globale Operation
  
    $$
    h(x,y)=F[g(x,y);i=0,\cdots,N;j=0,\cdots,M\}]
    $$
    

### 4.6.1.2 Glättungsfilter

Ziel: Glättung des Bildinhaltes, Rauschunterdrückung, Tiefpassfilterung

- Lineare Filter
    - **Box-Filter**
      
        $$
        h(m,n)=\sum\limits_{k,l}{g(k,l)f(m+k,n+l)} \\
        \text{z.B.} \quad
        \frac{1}{9}
        \begin{pmatrix}
        1 & 1 & 1\\
        1 & 1 & 1\\
        1 & 1 & 1
        \end{pmatrix} \quad
        \frac{1}{25}
        \begin{pmatrix}
        1 & 1 & 1 & 1 & 1\\
        1 & 1 & 1 & 1 & 1\\
        1 & 1 & 1 & 1 & 1\\
        1 & 1 & 1 & 1 & 1\\
        1 & 1 & 1 & 1 & 1
        \end{pmatrix}
        $$
        
        Vorteil: geringe Rechenkomplexität, z.B. mit Separierung und rekursiver Filterung
        
        Smoothing with box filter:
        
        ![4_Signalorientierte%20Bildverarbeitung/Untitled%2020.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2020.png)
        
    - **Binomial-Filter**
        - Faltung: Binmialfilter * Binomialfilter → Binomialfilter
        - 2D-Mask ist separierbar
        
        $$
        B_2=
        \begin{pmatrix}
        1& 2& 1\\
        2& 4& 2\\
        1& 2& 1\\
        \end{pmatrix}
        $$
        
        Vergleich zu Boxfilter: bessere Approximation eines Tiefpassfilters
        
    - **Gauss-Filter**
        - Faltung: Gaussfilter * Gaussfilter→Gaussfilter: $g(\sigma)*g(\sigma) \rightarrow g(\sqrt{2}{\sigma})$
        - 2D-Maske ist separierbar
        - Diskrete Approximation über Binomialfilter
        
        Weight contributions of neighboring pixels by nearness
        
        $$
        f(x,y)=\frac{1}{2\pi \sigma^2} e^{-\frac{x^2+y^2}{2\sigma^2}}
        \Leftrightarrow
        F(\omega_1,\omega_2)=e^{-\frac{1}{2}\sigma^2(\omega_1^2+\omega_2^2)}
        $$
        
        ![4_Signalorientierte%20Bildverarbeitung/Untitled%2021.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2021.png)
        
        Smoothing with Gaussian filter:
        
        ![4_Signalorientierte%20Bildverarbeitung/Untitled%2022.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2022.png)
    
- Nichtlinearer Filter
    - **Median-Filter**

![4_Signalorientierte%20Bildverarbeitung/Untitled%2023.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2023.png)

### 4.6.1.3 Kantenfilter

<aside>
💡 **Was ist Kantenfilter?**

Ein Kantenfilter in der digitalen Bildverarbeitung ist ein Filter, der dazu verwendet wird, Kanten und Kanteninformationen in einem Bild zu erkennen und zu verstärken. Einige Beispiele für Kantenfilter sind der Sobel-Filter, der Roberts-Filter und der Laplace-Filter.

</aside>

- **Motivation**
  Vorverarbeitungsschritt für Bildinterpretation
    - Kantendetektion: Canny‐Edge
    - Kantendetektion, Hough‐Transformation zur Detektion von Kreisen
    - Gradienten an Bildkanten:
      HOG‐Feature (Histogram of Gradients) als Merkmal für die Mustererkennung
  
    <aside>
    💡 **Wie kann man die Kantenstrukturen bestimmen?**
  
    Über die Differentiation der Grauwertfunktion
  
    </aside>
  
    1. Ableitung: $h(x)=\frac{\partial{g(x)}}{\partial{x}}$
    2. Ableitung: $h(x)=\frac{\partial^2{g(x)}}{\partial{x^2}}$
  
    ![4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-16_22.43.47.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-16_22.43.47.png)
  
    **Filter 1. Ableitung der Grauwertfunktion:**
  
    Berechnung diskreter Gradient:
  
    ![4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-16_23.30.51.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-16_23.30.51.png)
  
    **Zweite Ableitung der Grauwertfunktion:**
  
    Ort der Kante entspricht Nulldurchgang der zweite Ableitung
  
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2024.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2024.png)
  
- **Sobel Operator**
  
    Berechnung der 1. Ableitung in Verbindung mit einer Glättung des Bildes
    
    $$
    dx = \frac{1}{8}
    \begin{bmatrix}
    -1 & 0 & 1\\
    -2 & 0 & 2\\
    -1 & 0 & 1\\
    \end{bmatrix} \quad
    dy = \frac{1}{8}
    \begin{bmatrix}
    -1 & -2 & -1\\
    0 & 0 & 0\\
    1 & 2 & 1\\
    \end{bmatrix}
    $$
    
- **Prewitt Operator**
  
    $$
    dx = \frac{1}{6}
    \begin{bmatrix}
    -1 & 0 & 1\\
    -1 & 0 & 1\\
    -1 & 0 & 1\\
    \end{bmatrix} \quad
    dy = \frac{1}{6}
    \begin{bmatrix}
    -1 & -1 & -1\\
    0 & 0 & 0\\
    1 & 1 & 1\\
    \end{bmatrix}
    $$
    
- **Kirsch Operator**
  
    Liefert Faltungskerne für unterschiedliche Richtungen
    
    $$
    d_1 = \frac{1}{30}
    \begin{bmatrix}
    3 & 3 & 3\\
    3 & 0 & 3\\
    -5 & -5 & -5\\
    \end{bmatrix} \quad
    d_2 = \frac{1}{30}
    \begin{bmatrix}
    3 & 3 & 3\\
    -5 & 0 & 3\\
    -5 & -5 & 3\\
    \end{bmatrix} \quad
    d_3 = \frac{1}{30}
    \begin{bmatrix}
    -5 & 3 & 3\\
    -5 & 0 & 3\\
    -5 & 3 & 3\\
    \end{bmatrix}
    $$
    
- **Eigenschaften von Kantenfilten**
  
    Ziel: Detektion von Kanten, Hoch‐ bzw. Bandpassfilter
    
    - Symmetrieeigenschaft
      keine örtlich Verschiebung der Kante
      
      $$
        f(i)=-f(-i)
      $$
      
    - Unterdrückung des Mittelwertes
      
        $$
        1D: \quad \sum_i{f(i)}=0 \Leftrightarrow F(0)=0\\
        2D: \quad \sum_i\sum_j{f(i,j)}=0 \Leftrightarrow F(0,0)=0
        $$
        
    - Transferfunktion: 1D: (2R+1 Filtermaske)
      
        $$
        F(k)=2j\sum_{i=0}^R{f_i\sin{\left[\frac{2\pi ik}{N}\right]}}
        $$
        

![4_Signalorientierte%20Bildverarbeitung/Untitled%2025.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2025.png)

- **Laplace Operator**
  
    $$
    L=
    \begin{bmatrix}
    1 & 2 & 1\\
    2 & -12 & 2\\
    1 & 2 & 1
    \end{bmatrix}
    $$
    
    Praktisch:
    
    - Rauschen hat großen Einfluss
    - Nulldurchgang der 2. Ableitung ist schwer bestimmbar
- **LOG‐Filter: Laplacian of Gaussian / Marr‐Hildreth‐Operator**
    - Zuerst Glättung mit Gauß‐Filter
    - Anschließend Berechnung des Laplace‐Filters
    - Gauß‐Funktion: $G(x,y,\sigma)=\frac{1}{2\pi\sigma^2}e^{-\frac{x^2+y^2}{2\sigma^2}}$
    - Laplace‐Operation: $\nabla^2f=\frac{\partial^2f}{\partial x^2}+\frac{\partial^2f}{\partial y^2}$
    - Ergebnis ist die analytische Beschreibung des LOG‐Filters:$\nabla^2G(x,y,\sigma)=-\frac{1}{\pi\sigma^4}e^{-\frac{x^2+y^2}{2\sigma^2}}(1-\frac{x^2+y^2}{2\sigma^2})$
    
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2026.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2026.png)
    
- **DOG‐Filter: Difference of Gaussian**
  
    Approximation LOG, Anwendung in Bildpyramiden
    
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2027.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2027.png)
    

### 4.6.1.4 Sharpening Filter

Grundkonzept: Detektion von Grauwertänderungen und Verstärkung der Veränderungen

1. Sharpening mit Laplace‐Filter
   
    $$
    g(x,y)=f(x,y)+c[\nabla^2f(x,y)]
    $$
    
    ![4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-17_14.21.26.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-17_14.21.26.png)
    
2. “Unsharp-Masking” (Unsharpening-Filter)
    - Glatten Originalbild f(x, y)
    - Differenz Originalbild mit geglattetem Bild → Maske
    - Addition Maske zum Original
    
    $$
    g_{mask}(x,y)=f(x,y)-\overline{f}(x,y) \\
    g(x,y)=f(x,y)+K \cdot g_{mask}(x,y)
    $$
    
    ![4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-17_14.22.51.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-17_14.22.51.png)
    

Schärfungseffekt:

![4_Signalorientierte%20Bildverarbeitung/Untitled%2028.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2028.png)

## Zusammenfassung

![4_Signalorientierte%20Bildverarbeitung/Untitled%2029.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2029.png)

Lineare separierbare Filter und zugehörige Fourier‐Transformation:

![4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-17_14.33.26.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-05-17_14.33.26.png)

- Filtertypen
    - Glättungsfilter
    - Kantenfilter
    - Sharpening‐Filter
    - Globale Filter
- Motivation, Eigenschaften
- Charakterisierung im Frequenzbereich

## 4.6.2 Globale Filterung im Frequenzraum

- Homomorphe Filterung
  
    Ziel: Beleuchtung/Kontrast im Bild verbessern
    
    Idee:
    
    - Beleuchtungseffekte variieren langsam
    - Reflexionseffekte schnell
    
    Modell für die Bildentstehung: f(x, y) = i(x, y)+r(x, y)
    
    - i(x, y) Beleuchtungsanteil: Annahme hauptsächlich niederfrequente Anteile
    - r(x, y) Reflexionsanteile: Annahme hauptsächlich hochfrequente Anteile
    
    Filterung:
    
    - Logarithmierung, um eine additive Überlagerung beider Anteile zu erhalten
      
        f’(x, y) = log(i(x, y)) + log(r(x, y))
        
        FT[f’(x, y)] = FT[log(i(x, y))] + FT[log(r(x, y))]
        
    - Anwendung eines Filters H(k, l), der niederfrequente Anteile unterdrückt
    - Rücktransformation (und Anwendung von exp) ergibt gefiltertes Bild g(x, y)
    
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2030.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2030.png)
    
    Nachbearbeitung:
    
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2031.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2031.png)
    
    > **What is Homomorphic filtering? Reply by ChatGPT**
    > 
    > 
    > Homomorphic filtering is a technique used in image processing to enhance images by adjusting the lighting conditions while preserving the overall shape and details of the objects in the image. It is particularly effective for images that suffer from uneven lighting or variations in illumination.
    > 
    > The main idea behind homomorphic filtering is to decompose the image into its low-frequency and high-frequency components. The low-frequency component represents the illumination or lighting variations, while the high-frequency component represents the details and edges in the image.
    > 
    > The homomorphic filter applies a logarithmic transformation to the low-frequency component, which compresses the dynamic range of the illumination variations. Then, a high-pass filter is applied to the high-frequency component to amplify the details and edges.
    > 
    > By performing the filtering in the logarithmic domain, the homomorphic filter is able to adjust the lighting conditions without distorting the image's details. It effectively enhances the image by reducing the influence of lighting variations while preserving the important information.
    > 
- Notch‐Filter
  
    Aufgabe: Unterdrückung ausgewählter Frequenzen
    

## 4.6.3 Bildrestauration, Inverse Filterung

- Inverses Filter
    1. **Faltungsinversion mit inversem Filter**
        - Beschreibung der Abbildung im Orts‐ und Frequenzbereich
          
            $$
            f''(x,y) = h(x,y) * f(x,y) + r(x,y) \\
            F''(u,v) = H(u,v) * F(u,v) + R(u,v)
            $$
            
        - Inverse Filterung ohne Rauschen
          
            $$
            \hat{F}(u,v)=\frac{F''(u,v)}{H(u,v)}
            \text{ bzw. }
            Q(u,v)= \frac{1}{H(u,v)}
            $$
            
        - Inverse Filterung mit Einbeziehung des Rauschens
          
            $$
            \hat{F}(u,v)=\frac{H(u,v)*F(u,v)+R(u,v)}{H(u,v)}
            =F(u,v) + \frac{R(u,v)}{H(u,v)}
            $$
            
        
        Idee: Inversion ohne Berücksichtigung des Rauschens
        
        **Problem**
        
        - Nullstellen der Transferfunktion H(u, v)=0
        - Starke Verstärkung des Rauschens → Ergebnis praktisch kaum brauchbar
    2. **Inverses Filter mit Unterdrückung der „Polstellen“**
        - Umgehung des Problems „Nullstellen“ der Transferfunktion H(u, v)
        - Modifizierte inverse Filterung:
        
        $$
        Q(u,v) =
        \left\{
        \begin{aligned}
        &\frac{1}{H(u,v)} \quad :|H(u,v)|>\epsilon \\
        &0 \quad : \text{sonst}
        \end{aligned}
        \right.
        $$
        
        - Fourierkoeffizienten mit zu kleinem Betrag werden in der Berechnung des inversen Filters nicht berücksichtigt
    3. **Faltungsinversion mit Wiener Filter**
    - Idee:
        - Stochastische Modellierung von Bild und Rauschen
        - Lösung der Minimierungsaufgabe
            - Suche ein Filter $q(x,y)$ das den Erwartungswert E des quadratischen Fehlers zwischen gemessenen Bild $f''(x,y)$ und Originalbild $f(x,y)$ minimiert
            
            $$
            E[(f(x,y)-q(x,y)*f''(x,y)^2] \rightarrow \min
            $$
    
- Wiener Filter
  
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2032.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2032.png)
    
    - **Autokorrelationsfunktion: Die stochastische Modellierung**
      
        > **Was ist Autokorrelation?**
        > 
        > 
        > Autokorrelation: Die stochastische Modellierung des Bildes im Wiener‐Filter
        > 
        > - Autokorrelationsfunktion beschreibt die statistische Abhängigkeit zwischen jeweils zwei Pixeln des Bildes in Abhängigkeit von ihrer Lage zueinander
        >     
        >     $$
        >     \phi_{ff}(i,j)=E[(f(x,y)-E[f(x,y)]) \cdot (f(x+i,y+i)-E[f(x+i,y+i)])]
        >     $$
        >     
        > - Eine Realisierung der Autokorrelation eines Bildsignales kann aus dem Bildsignal über die diskrete Autokorrelation selbst berechnet werden
        >     
        >     $$
        >     \phi_{ff}(i,j)=\frac{1}{N}\frac{1}{M} \sum\limits_{x=0}^{N-1} \sum\limits_{y=0}^{M-1} f(x,y)f(x+i,y+i) = (f * f^S)_{i,j}
        >     $$
        >     
        >     - Dies ist als Faltung mit Signals $f$ mit gespiegeltem Signal $f^S$ darstellbar
    - **Lösung Optimierung und Eigenschaften**
      
        Lineares Signalmodell:
        
        $$
        f''(x,y)= h(x,y) * f(x,y) + r(x,y)
        $$
        
        Lösung des Optimierungsproblems zur Suche des Filters q(x,y):
        
        $$
        E[(f(x,y)-q(x,y)*f''(x,y)^2] \rightarrow \min
        $$
        
    - **Praktische Umsetzung**
      
        $$
        Q(u,v)=\frac{1}{H(u,v)} \cdot \frac{|H(u,v)|^2}{|H(u,v)|^2 + \frac{S_{rr}(u,v)}{S_{ff}(u,v)}}
        $$
        
        - Rauschfreie Abbildung $(S_{rr}=0)$ ergibt das inverse Filter $Q(u,v)=\frac{1}{H(u,v)}$
        - Nullstellen der Transferfunktion $H(u, v) = 0$ führen bei $(S_{rr}(u, v) > 0)$ auf $Q(u,v) = 0$, Filterantwort für alle Frequenzen $u, v$ immer berechenbar, keine Verstärkung des Rauschens
        - Leistungdichtespektrum des Rauschen $S_{rr}=\sigma_r^2$, als Konstante
        - Leistungsdichtespektrum des Bildes (mögliche Varianten):
            - Bestimmung aus dem Bild selbst $S_{ff}(u,v)=|F(u,v)|^2 - \sigma_r^2$
            - allgemeines Modell
            - funktional, z.B. $S_{ff}=\sigma_f^2 \rho^{-\sqrt{u^2+v^2}+\overline{f}^2}$ mit $\overline{f}$ als Mittelwert des Bildes und $\sigma_f,\rho$ als Parameter
        - Systemfunktion $H(u,v)$ aus Systemmodellierung oder experimentellen Untersuchungen
        
        Weitere vereinfachende Annahme:
        
        $$
        k=\frac{S_{rr}(u,v)}{S_{ff}(u,v)}
        $$
        
        Ergebnis: „Heuristisches Wiener‐Filter“
        
        $$
        Q(u,v)=\frac{1}{H(u,v)} \cdot \frac{|H(u,v)|^2}{|H(u,v)|^2 + k}
        $$
    
- Inverses Filter v.s. Wiener Filter
    - Anwendungen von Inverses Filter und Wiener Filter:
    um Bild- oder Signalverzerrungen zu korrigieren und die ursprünglichen Informationen wiederherzustellen.
    - Nullsetlleproblem:
      
        逆滤波器的零点问题是指在使用逆滤波器进行图像恢复时可能遇到的困难。具体而言，当原始图像中存在特定频率的零点时，逆滤波器会产生问题。
        
        在图像处理中，零点是指频域中的频率，其振幅为零。当逆滤波器应用于包含零点的图像时，它会导致输出结果无法准确地恢复原始图像的信息。这是因为逆滤波器试图在频域中将零点处的幅度恢复为无穷大，从而引入了不稳定性和非物理性的估计结果。
        
        逆滤波器的零点问题在实际应用中是一个挑战，特别是当图像中存在大量噪声或频域中存在较低幅度的细节时。解决这个问题的方法之一是通过引入正则化技术或约束条件来限制逆滤波器的幅度增长，并防止输出结果受到零点的影响。
        
        需要注意的是，逆滤波器的零点问题是由图像中的特定频率分量引起的，并且可能因图像内容和噪声特性而异。因此，在实际应用中，需要仔细分析图像的频域特征，并根据具体情况选择合适的滤波器设计和参数调整来解决零点问题。
        
        维纳滤波器通过在频域中将滤波操作分为两个部分来处理问题：信号部分和噪声部分。维纳滤波器首先对信号进行逆滤波，以尽可能恢复原始信号的细节。然后，它引入一个补偿项，该项根据噪声的统计特性和信噪比来调整滤波结果。这个补偿项可以有效地抑制零点处的不稳定性，并控制滤波结果的增益，从而提供更好的图像恢复效果。
        
    - Vorteile und Nachteile
        - Vorteile des inversen Filters:
            - Einfache Konzeption und Implementierung
        - Nachteile des inversen Filters:
            - Empfindlich auf Rauschen und Fehler, da er dazu neigt, Rauschen zu verstärken.
            - Kann instabil sein, insbesondere wenn das gestörte Signal eine geringe Signal-zu-Rausch-Verhältnis (SNR) aufweist.
        - Vorteile des Wiener Filters:
            - Bietet eine bessere Rauschunterdrückung und Signalwiederherstellung im Vergleich zum reinen inversen Filter.
            - Berücksichtigt sowohl das Signal als auch das Rauschen, um eine optimale Filterung zu erreichen.
            - Kann die Bild- oder Signalqualität verbessern, indem es Rauschen reduziert und Details besser erhält.
        - Nachteile des Wiener Filters:
            - Erfordert Kenntnisse über die statistischen Eigenschaften des Signals und des Rauschens, um optimale Filterparameter zu bestimmen.
            - Funktioniert möglicherweise nicht gut bei nicht-stationärem Rauschen oder wenn die statistischen Eigenschaften des Signals und des Rauschens sich im Laufe der Zeit ändern.

## Zusammenfassung

- Lineares Modell zur Bildverzerrung
- Inverses Filter
- Wiener Filter
    - Stochastische Modellierung
    - Autokorrelationsfunktion
    - Lösung Optimierung und Eigenschaften
    - Praktische Umsetzung

# 4.7 Unitäre Transformationen: DCT, Hadamard‐, Haar‐, Wavelet‐Transformation

Motivation aus Anwendungssicht:

- Bildkompression
- Merkmalsberechnung für Bildsegmentierung, Tracking, Klassifikation

### Diskrete Kosinus Transformation (DCT)

- **Diskrete Kosinus Transformation (DCT) 1D & 2D**
    - 1-dimesional:
      
        $$
        DCT_k = \frac{2}{\sqrt{2N}} \sum\limits_{i=0}^{N-1} f_i \cdot \bigg[ \frac{k\pi(2i+1)}{2N} \bigg]
        $$
        
    - 2-dimensional:
      
        $$
        DCT_{k,m} = \frac{2}{\sqrt{2N}} \frac{2}{\sqrt{2M}} \sum\limits_{x=0}^{N-1} \sum\limits_{y=0}^{M-1} f_{x,y} \cdot
        \bigg[ \frac{k\pi(2x+1)}{2N} \bigg]
        \bigg[ \frac{m\pi(2y+1)}{2M} \bigg]
        $$
    
- **Anwendungen der DCT:**
    - Bildkompression (JPEG, MPEG1/2/4, AVC, HEVC, VVC, Ausnahme JPEG 2000)
    - Modifizierte DCT für Audiokompression in MP3
    - DCT besitzt reellwertige Basisfunktionen:
        - Nachteil für Umsetzung in Hardware wg. aufwändiger Arithmetik (float)

### Hadamard‐Transformation

[Hadamard transform](https://en.wikipedia.org/wiki/Hadamard_transform)

- **1D Hadamard‐Transformation**
  
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2033.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2033.png)
    
- **2D Hadamard‐Transformation**
  
    Komplexität O(N*N)
    
    Hadamard‐Koeffizienten = Transformation * Signal
    
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2034.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2034.png)
    
    - 2D‐Basisfunktion aus 1D‐Basisfunktionen $h_{i,j}=h_ih_j^T$
    - Beispiel (Indizes nach sequenzieller Ordnung, siehe nächste Folie):
      
        $$
        \mathrm{h}_{12} =
        \begin{pmatrix}
        1 \\ 1 \\ -1 \\ -1
        \end{pmatrix}
        \cdot
        \begin{pmatrix}
        1 & -1 & -1 & 1
        \end{pmatrix}
        \begin{pmatrix}
        1 & -1 & -1 & 1\\
        1 & -1 & -1 & 1\\
        -1 & 1 & 1 & -1\\
        -1 & 1 & 1 & -1
        \end{pmatrix}
        $$
        
    - Vorteile:
        - Separierbare Transformation
        - Zeilen/Spaltenweise Transformation
        - Schnelle Berechnung
- **Anwendungen Hadamard Transformation**
    - Bildkompression (JPEGXR)
    - H.264/MPEG‐4 Part 10 or AVC (Advanced Video Coding)
    - Data encryption
    - Signal processing
    - Data compression

### Gefensterte Fourier‐Transformation

- **Transformationen mit Orts‐ und Frequenzzuordnung**
    - Fourier‐Transformation:
    Basisfunktionen (Sinus‐Wellen) über gesamtes Bild ausgedehnt → keine Ortszuordnung der Fourierkoeffizienten
    - Wunsch:
    Transformation, die Orts‐ und Frequenzzuordnung der Transformationskoeffizienten erlaubt
    - Ziel:
    Basisfunktionen mit örtlich begrenzter Ausdehnung → z.B. für lokale Charakterisierung
    Bildinhalte → z.B. für die Textursegmentierung
- **1D Gefensterte Fourier‐Transformation**
  
    ![4_Signalorientierte%20Bildverarbeitung/Untitled%2035.png](4_Signalorientierte%20Bildverarbeitung/Untitled%2035.png)
    
- **2D Gefensterte Fourier‐Transformation**
  
    Fensterfunktion
    
    - Fourier‐Transformation mit Gauß‐Funktion gewichtet → Gabor‐Funktion im Ortsbereich
    
    Gabor‐Filter analysieren orientierte Strukturen bestimmter Größe
    
    ![4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-06-26_23.44.33.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-06-26_23.44.33.png)
    
    **Anwendungsbeispiel: Gabor Filter**
    

### Wavelet Transformationen

- Motivation
Transformation des Bildes in Frequenzraum mit zusätzlicher Ortsinformation
- Eigenschaften
    - Transformation ist umkehrbar (invertierbar)
    - Erhaltung der Energie
    - Verdichtung der Energie
- Einfachste Variante: Haar Transformation
- Anwendungen
    - Bildkompression (JPEG 2000)
    - Signalverarbeitung

### Haar Transformation

[哈尔小波变换 - 维基百科，自由的百科全书](https://zh.wikipedia.org/zh-cn/%E5%93%88%E7%88%BE%E5%B0%8F%E6%B3%A2%E8%BD%89%E6%8F%9B)

- **Haar‐Transformation (1D)**
  
    $$
    H^{(N)}_{ij}:=
    \begin{cases}
    \frac{1}{\sqrt{2}}, \quad 
    &\text{if } i\leq\frac{N}{2},j\in\{2i-1,2i\}\\
    
    \frac{1}{\sqrt{2}}, \quad 
    &\text{if } i>\frac{N}{2},j=2(i-\frac{N}{2})-1\\
    
    -\frac{1}{\sqrt{2}}, \quad 
    &\text{if } i>\frac{N}{2},j=2(i-\frac{N}{2})\\
    0, \quad
    &\text{otherwise}
    \end{cases}
    $$
    
    - Orthonormale Basis
    - Örtliche begrenzte Ausdehnung der Basisfunktionen
    - einfache Berechnung

![Untitled](4_Signalorientierte%20Bildverarbeitung/Untitled%2036.png)

- **Anwendung Haar‐Transformation: Kompression + Denoising**
  
    a) Signal
    
    b) 12‐level Haar‐Transformation
    
    c) Koeffizienten kleiner als ein Schwellwert auf Null gesetzt
    
    d) Rücktransformiertes Signal
    
    ![4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-06-27_00.42.18.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-06-27_00.42.18.png)
    

<aside>
💡 **Was unterscheidet die Haar‐ von der Hadamard‐Transformation?**

Bei der Hadamard Transformation werden auch die hochpassgefilterten Bildanteile „weiterverarbeitet“. Die Haar Transformation behält dort ihren „lokalen Charakter“.

</aside>

## Zusammenfassung

- Hadamard-Transformation
    - Bildkompression (AVC - nur DC-Koeffizienten der DCT)
    - Merkmale für die Mustererkennung
- DCT
    - Bildkompression (JPEG, H.261, MPEG-1, MPEG-2 (H.262), H.263, MPEG-4, AVC (H.264), HEVC (H.265), VVC (H.266))
- Haar-Transformation
    - Bildkompression
    - Merkmale für die Mustererkennung
- Wavelet-Transformation
    - Bildkompression

## 4.8 Bildpyramiden und Multiresolutiondarstellung

<aside>
💡 **Was is Gaußpyramide in digitaler Bildverarbeitung?**

In digital image processing, a Gaussian pyramid (Gaußpyramide) is a multi-scale representation of an image where each level of the pyramid is a smoothed and downsampled version of the previous level. It is created by applying a Gaussian filter to the original image and then subsampling it to reduce its size. The Gaussian pyramid allows for efficient computation at different image scales and is commonly used in tasks such as image blending, image compression, and image pyramids for object detection and recognition.

</aside>

- Gausspyramide
    - Stufe I → Stufe I+1
    - Tiefpassfilterung → Unterabtastung → I+1
    - Speicherbedarf einer Bildpyramide
        - $M^2 = \text{Anzahl der Pixel}$
        - Unterabtastung je Stufe und Dimension um den Faktor 2
        
        $$
        M^2(1+\frac{1}{4}+\cdots+\frac{1}{4^N}+\cdots)=M^2(1+\frac{1}{3})
        $$
        
    - Anwendung
        - Optischer Fluss
            - Bewegungsvektor
                - Sysematische Suche(Blockmatching)
                - SAD(Sum of Absolut Differences) als Fehlerkriterium
        - Multi-Scale Flow Estimation
            - Reduzierung Rechenaufwand
            - Erhöhung Robustheit
            - Schätzung langer Bewegungsvektoren
- Laplace-Pyramide
    - Grundkonzept: Speicherung der Differenzen zwischen den verschiedenen Leveln der Gausspyramide
    - Result = Origial image -new image (Filterung + Unterabtastung)
      
        ![截屏2023-07-15 03.46.04.png](4_Signalorientierte%20Bildverarbeitung/%25E6%2588%25AA%25E5%25B1%258F2023-07-15_03.46.04.png)
        
    - Rekonstruktion Bildsignal einer Gauss-Pyramidenstufe
        - Expansion Bildgröße um Faktor 2
        - Einführung von Nullen auf Zwischenpositionen und Filterung
    - Unterschiede Bildpyramide zu Waveletzerlegung
      
      
        - Laplace-Pyramide
            - Redundante Repräsentation
                - keine orientierungsabhängige Filterung des Bildinhaltes
        
        - Orthogonale Waveletzerlegung
            - kompakte Repräsentation, da Anzahl der Bildpunkte gleich Anzahl Koeffizienten
            - Waveletkoeffizienten sind Orientierungsabhängig
- **Anwendung Bildpyramiden**
    - Datenkompression
    - Reduzierung des Rechenaufwandes
    - Merkmalsdetektion von Kanten, markante Punkten
    - Blending (Überblenden von Bildinhalten)