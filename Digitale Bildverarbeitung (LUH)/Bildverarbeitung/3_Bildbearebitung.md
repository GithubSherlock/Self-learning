# 3_Bildbearebitung

Created: July 13, 2023 3:12 PM

# 3_Bildbearebitung

## Zusammenfassung

- **Klassen von Operationen**
    - Punktoperationen
    - Lokale Operationen
    - Globale Operationen
- **Punktoperationen**
    - Ein Bild: Kontrastverbesserung, Histogrammausgleich, ...
    - Mehrere Bilder: Bildmittelung, ...
- **Lokale Operationen**
    - Lineare Filter
    - Nichtlineare Operationen
- **Globale Operationen**
- **Geometrische Transformationen**

# 3.1 Klassen von Operationen

Motivation:

- Verbesserung von Bildern für visuelle Darstellung oder nachfolgende Bildinterpretationsschritte
    - z.B. Änderung Helligkeit, Kontrast, Farbkorrektur, „Schärfen“
- Modifikation von Bildern für nachfolgende Bildinterpretation
    - z.B. Kantenfilter, Binärisierung, ...

![Untitled](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/Untitled.png)

# 3.2 Punktoperationen - Intensitätstransformationen

### (Nicht-)Lineare Punktoperationen

Lineare Punktoperation: $h(x,y)=A \cdot g(x,y) + B$

Nichtlineare Punktoperation: z.B. Kennlinie

- Gamma-Korrektur

![Untitled](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/Untitled%201.png)

### Grauwert-Histogramme und Histogrammausgleich

**Grauwert-Histogramme:**

$$
n(i)= \operatorname{Anzahl}[g(x,y)=i]
$$

![截屏2023-05-10 21.11.38.png](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/%25E6%2588%25AA%25E5%25B1%258F2023-05-10_21.11.38.png)

**Histogrammspreizung:**

$$
h(x,y)=255 \cdot \frac{g(x,y)-g_{min}}{g_{max}-g_{min}}
$$

![截屏2023-05-10 21.11.52.png](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/%25E6%2588%25AA%25E5%25B1%258F2023-05-10_21.11.52.png)

**Histogrammausgleich**

Histogramm:

$$
n(i),i=1,\cdots,I
$$

Kumuliertes Histogramm:

$$
N(i)=\sum\limits_{k=0}^i n(k)
$$

LUT

$$
N'(i) = \operatorname{round}
\left[
I\frac{N(i)}{N(I)}
\right]
$$

Transfer der Grauwerte

$$
h(x,y)=N'[g(x,y)]
$$

### Punktoperationen an mehreren Eingangsbildern

![Untitled](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/Untitled%202.png)

### Zusammenfassung Punktoperationen

$$
h(x,y)=F[g(x,y)];
$$

Punktoperationen mit einem Eingangsbild

- Lineare Punktoperation
    
    $$
    h(x,y)=A \cdot g(x,y)+B
    $$
    
- Nichtlineare Punktoperation
    - Gammakorrektur
- Histogramme zur Bestimmung von Bildeigenschaften
    - Histogrammspreizung
    - Histogrammausgleich
- Schwellwertbildung

Punktoperationen mit mehreren Eingangsbildern

Look-Up Tabellen zur schnellen Bildtransformation

# 3.3 Lokale Operationen - Filterung

$$
h(x,y)=F[\{g(x+i,y+j);i=I_1,\cdots,I_2;j=J_1,\cdots,J_2\}]
$$

### 3.3.1 Lineare Filter

Einführung linearer Filter

**Box Filter (Glättungseffekt)**

$$
h(m,n)=\sum\limits_{k,l}{g(k,l)f(m+k,n+l)} \\
\text{z.B.} \quad 
\frac{1}{9}
\begin{bmatrix}
1 & 1 & 1\\
1 & 1 & 1\\
1 & 1 & 1
\end{bmatrix}
$$

Aufgaben:

- Replaces each pixel with an average of its neighborhood
- Achieve smoothing effect (remove sharp features)

**Sharpening filter (Schärfungseffekt)**

- Accentuates differences with local average

**Edge Detection**

Sobel Filter

$$
\begin{equation*}
S_x = \begin{bmatrix}
-1 & 0 & 1 \\
-2 & 0 & 2 \\
-1 & 0 & 1
\end{bmatrix}
\quad
S_y =
\begin{bmatrix}
-1 & -2 & -1\\
0 & 0 & 0\\
1 & 2 & 1
\end{bmatrix}
\end{equation*}
$$

**Filtering v.s. Convolution**

g = filter/convolution mask, f = input image, h = output image

- 2D Filtering
    
    $$
    h(x,y)=\sum\limits_{k,l}{g(k,l)f(x+k,y+l)}
    $$
    
    ```matlab
    h = filter2(g, f); % or
    h = imfilter(f, g);
    ```
    
- 2D Convolution („Faltung“)
    
    $$
    h(x,y)=\sum\limits_{k,l}{g(k,l)f(x-k,y-l)}
    $$
    
    ```matlab
    h = conv2(g, f);
    ```
    

<aside>
💡 What difference between Filtering and Convolution in digital image processing?

In digital image processing, filtering and convolution are related concepts, but they have some important differences.

Filtering refers to the process of modifying or enhancing an image by applying a filter, which is a mathematical function that operates on the pixel values in the image. Filters can be designed to achieve a variety of goals, such as smoothing, sharpening, edge detection, or noise reduction.

Convolution is a specific mathematical operation that is commonly used in filtering. Convolution involves sliding a kernel (also known as a filter or mask) over the image and computing a weighted sum of the pixel values in each local neighborhood of the image. The result of the convolution operation is a new image where each pixel value is a weighted average of the neighboring pixel values in the original image. Convolution is a fundamental operation in digital image processing and is used in many different applications.

In summary, filtering is a general term that encompasses a wide range of image processing operations, including convolution, while convolution is a specific operation that is often used as part of a filtering process.

</aside>

**Weitere Eigenschaften linearer Filter**

![Untitled](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/Untitled%203.png)

<aside>
💡 Wie viele **Multiplikationen** und **Addition** werden bei einer Faltung mit der folgenden Filtermaske pro Pixel benötigt?

Multiplikationen: m*n
Additionen: m*n-1

z.B.: $\begin{bmatrix}
1 & 4 & 6 & 4 & 1\\
\end{bmatrix}$
Multiplikationen: 5
Additionen: 4

</aside>

> What about near the edge?
> 
> - the filter window falls off the edge of the image
> - need to extrapolate
> - Methods:
>     - clip filter (black)
>     - wrap around
>     - copy edge
>     - reflect across edge
>     
>     ```matlab
>     imfilter(f, g, 0); % clip filter (black)
>     imfilter(f, g, 'circular'); % wrap around
>     imfilter(f, g, 'replicate'); % copy edge
>     imfilter(f, g, 'symmetric'); % reflect across edge
>     ```
>     

**Practical matters**

![Untitled](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/Untitled%204.png)

### 3.3.2 Nichtlineare Filter

**Median Filter**

![Untitled](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/Untitled%205.png)

**Gradientenfilter**

![Untitled](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/Untitled%206.png)

<aside>
💡 What is gradient filter?

A gradient filter, also known as a derivative filter, is a type of image filter used in digital image processing to compute the image gradient, which measures the rate of change of the image intensity. Gradient filters are commonly used for edge detection and feature extraction tasks, as edges and features often correspond to regions of rapid intensity changes in an image. Gradient filters can be implemented in a variety of ways, such as by using convolution with a filter kernel or by using discrete differentiation operators. The resulting gradient image can be used to extract features, compute optical flow, or perform other types of image analysis.

</aside>

## Zusammenfassung Lokale Operationen

Lineare Filter

- Box filter
- Sharpening
- Edge detection
- Filtering vs. Convolution
- Eigenschaften linearer Filter (Linearität, Verschiebungsinvarianz, …)
- Separierbarkeit

Nichtlineare Filter

- Medianfilter
- Gradientenfilter

# 3.4 Globale Operationen

Zwei Beispiele für globale Operationen

- Fourier-Transformation
- Hadamard-Transformation

# 3.5 Geometrische Transformationen

**Intensitätstransformation: z.B. Punktoperationen**

$$
h(x,y)=F[g(x,y)]
$$

![截屏2023-05-11 20.40.39.png](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/%25E6%2588%25AA%25E5%25B1%258F2023-05-11_20.40.39.png)

Modifikation Grau- oder Farbwerte des Pixels:

**Geometrische Transformation**

$$
h(T[x,y])=g(x,y)
$$

Modifikation der geometrischen Position des Pixels

![截屏2023-05-11 20.40.23.png](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/%25E6%2588%25AA%25E5%25B1%258F2023-05-11_20.40.23.png)

Anwendungen:

- Drehen, Skalieren von Bildern
- Kissen- und tonnenförmige Verzeichnung
- Korrektur von Skew und Slant in Dokumentbildern

![截屏2023-05-11 20.46.44.png](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/%25E6%2588%25AA%25E5%25B1%258F2023-05-11_20.46.44.png)

**Vorwärts- und Rückwärts-Transformation (forward and backward mapping)**

$$
\mathrm{x'=T[x]} \quad \mathrm{x=T^{-1}[x']}
$$

![截屏2023-05-11 21.21.24.png](3_Bildbearebitung%20ca332a961dcf4012ab83f2c9108f0281/%25E6%2588%25AA%25E5%25B1%258F2023-05-11_21.21.24.png)

### Zusammenfassung Geometrische Transformation und Interpolation

Punktoperation vs. geometrische Transformation

Vorwärts- und Rückwärts-Transformation

Interpolation der Pixelwerte

- Nächster Nachbar
- Bilinear
- Mitchell-Netravali-Filter (bikubisch)