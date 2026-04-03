# Wykład 4

## Twierdzenie o rekurencji uniwersalnej

Niech $a\geqslant 0$ i $b>0$ będą stałymi, niech $f(n)$ będzie pewną funkcją i niech $T(n)$ będzie zdefiniowane dla nieujemnych liczb całkowitych przez rekurencję:
$$
T(n)=aT(n/b)+f(n)
$$
gdzie $n/b$ oznacza $\lfloor n/b \rfloor$ lub $\lceil n/b \rceil$. Wtedy funkcja $T(n)$ może być ograniczona asymptotycznie w następujący sposób:

1. Jeśli $f(n)=O(n^{\log_b a - \varepsilon })$ dla pewnej stałej $\varepsilon >0$, to 
   $$
     T(n)=\Theta(n^{\log_b a})
   $$ 
2. Jeśli $f(n)=\Theta(n^{\log_b a })$ to:
   $$
     T(n)=\Theta(n^{\log_b a}\log n)
   $$ 
3. Jeśli $f(n)=\Omega(n^{\log_b a +\varepsilon})$ dla
    pewnej stałej $\varepsilon >0$, oraz $af(n/b)\leqslant c f(n)$  dla pewnych stałej $c<1$ i wszystkich dostatecznie dużych $n$, to:
   $$
    T(n)=\Theta(f(n))
   $$

## Uzasadnienie przypadku 1.

Dla $f(n)=0$ mamy 
$$ T(n)=aT(n/b)$$
zakładając, że $T(n)=c\cdot n^k $ możemy wyznaczyć $k$ w taki sposób:
$$ T(n)=aT(n/b)$$

$$ c\cdot n^k= a\cdot  c \cdot (n/b)^k $$
$$ 1= a/b^k $$
$$ b^k= a $$
$$ k= \log_b a $$
czyli:
$$ T(n)=c \cdot n^{\log_b a} =\Theta(n^{\log_b a})$$

Przypadek 1. mówi, że dopóki $f(n)$ jest ograniczone przez $n$ do potęgi mniejszej niż $\log_b a$, czyli $f(n)=O(n^{\log a -  \varepsilon})$, to ta złożoność pozostaje bez zmian.

Przykład: Dodawanie ma dwóch macierzy o wymiarach $n\times n$ wymaga $n^2$ dodawań więc złożoność wynosi $\Theta(n^2)$

Ten sam wynik możemy otrzymać pisząc procedurę rekurencyjną, która dodawanie macierzy $A$ i $B$ zrealizuje przez dodawanie odpowiednich ćwiartek o wymiarach $\frac n2 \times \frac n 2$. Otrzymana zalezność rekurencyjna: 
$$ T(n) =  4 T(n/2))$$ 
po skorzystaniu z Twierdzenia (przypadek 1.)  dla $a=4$, $b=2$, da nam poprawną złożoność:

$$T(n)=\Theta(n^{\log _b a})=\Theta(n^{\log_2 4})=\Theta(n^2)$$

## Uzasadnienie przypadku 2.

Załóżmy że:

 $$T(n)=aT(n/b) + c\cdot n^{\log _b a}$$

 wtedy

 $$T(n/b)=aT(n/b^2) + c\cdot (n/b)^{\log _b a}$$
 $$T(n/b)=aT(n/b^2) + c\cdot n^{\log _b a}/b^{\log _b a}$$
$$T(n/b)=aT(n/b^2) + c\cdot n^{\log _b a}/a$$

więc:

$$T(n)=a(aT(n/b^2) + c\cdot n^{\log _b a}/a)+ c\cdot n^{\log _b a}$$

$$T(n)=a^2T(n/b^2) + c\cdot n^{\log _b a}+ c\cdot n^{\log _b a}$$

na $k$_tym poziomie rekurencji będzie: 

$$T(n)=a^kT(n/b^k) + k\cdot c\cdot n^{\log _b a}$$

Rekurencja kończy się, gdy $n=b^k$ więc $k=\log_b n$ czyli: 

$$T(n)=a^{\log_b n}\cdot T(1) + \log_b n\cdot c\cdot n^ {\log _b a}$$

$$T(n)=n^{\log_b a}\cdot T(1) + \log_b n\cdot c\cdot n^ {\log _b a}$$

$$T(n)=n^{\log_b a} (T(1) + c\cdot \log_b n)$$

$$T(n)=\Theta(  n^ {\log _b a}\cdot \log n )$$

