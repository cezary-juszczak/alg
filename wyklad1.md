# Algorytmy i Struktury Danych
# Wykład 1- podstawowe pojęcia

* algorytm, algorytm poprawny, 
* złożoność czasowa/pamięciowa, średnia/pesymistyczna  
* notacje: $o$, $O$, $\Theta$.
* przykłady algorytmów: 
	  * największy wspólny dzielnik, 
	  * sito Erastotenesa,  
	  * mnożenie wielomianów, 
	  * schemat Hoernera, 
	  * wyszukiwanie binarne
* struktura danych, jako rozmieszczenie danych w pamięci: 
	  * tablice, 
	  * listy jednokierunkowe, 
	  * listy dwukierunkowe, 
	  * drzewa binarne.
* struktury danych jako zbiór operacji elementarnych: 
	  * stos (LIFO), 
	  * kolejka (FIFO), 
	  * find-insert, 
	  * find-insert-delete, 
	  * union-find

## Algorytm 
**Algorytm** to dokładny przepis (sposób postępowania) pozwalający, dla dowolnych danych wejściowych $(a_1, ..., a_n)$, otrzymać rozwiązanie $(b_1, ..., b_m)$ danego problemu.

**Uwaga:** Rozmiar danych wejściowych $n$ i rozmiar rozwiązania $m$ **nie muszą być równe**. 

**Przykłady:** 

1. Wyznacz wszystkie permutacje $k$ symboli.
    * Rozmiar danych $n=k$
    * Rozmiar wyniku $m=k\cdot k!$ 
2. Znajdź ilość wystąpień słowa w tekście:
    * Rozmiar danych $n=$ długość tekstu $+$ długość słowa
    * Rozmiar wyniku $m=1$ (jedna liczba) 

**Uwaga 2:** Każda rzecz w pamięci komputera  (nawet grafika, film) jest reprezentowana w pamięci komputera za pomocą ciągu liczb. Zatem nasza **definicja algorytmu** jest całkiem **ogólna**.      

### Algorytm poprawny  

**Algorytm poprawny** to algorytm, który dla dowolnych danych wejściowych:

1. **Kończy się** (nie wchodzi w nieskończoną pętlę ani nie zawiesza)
2. **Daje poprawny wynik**

### Przykłady algorytmów 

* Powszechnie stosowane (niekoniecznie komputerowe):
     * Dodawanie, odejmowanie, mnożenie, dzielenie pisemne
     * Rozwijanie ułamka zwykłego w dziesiętny (okresowy).
     * Wyznaczenie ilości dni miesiąca (kostki piąstek)
     * Mnożenie $i$ przez 9 (zgięcie $i$-tego palca)
     * Otwieranie książki na $i$-tej stronie (bisekcja)
* Komputerowe
    * Największy wspólny dzielnik (alg. Euklidesa) 
    * Sprawdzanie, czy liczba jest pierwsza 
    * Znajdź liczby pierwsze mniejsze niż $n$ (sito Erastotenesa)
    * Obliczanie wartości wielomianu $W$ w punkcie $x$ (schemat Hoernera)
    * Mnożenie, dzielenie, potęgowanie macierzy (alg. Strassena)
    * Mnożenie wielomianów (działanie na współczynnikach) (DFT)
    * Znalezienie w tablicy elementu maksymalnego w tablicy
    * Wyszukanie elementu $x$ w tablicy:
        * posortowanej
        * nieposortowanej 
    * Posortowanie tablicy (ustawienie elementów rosnąco wg wartości)
    * Mnożenie $n$-cyfrowych liczb całkowitych (dla dużych $n$) 
    * Przykłady algorytmów grafowych:
        * Sprawdzenie czy graf jest spójny
        * Sprawdzenie czy istnieje ścieżka z wierzchołka A do B
        * Znalezienie najkrótszej ścieżki z A do B
        * Znalezienie minimalnego drzewa rozpinającego.
        * Znalezienie drzewa najkrótszych ścieżek (np. Dijkstra)
    * Sprawdzenie, czy punkt zawiera się w wielokącie 
    * Znalezienie odległości punktu od wielokąta
    * Minimalna triangulacja wielokąta
### Algorytmy iteracyjne versus rekurencyjne

  * Wiele algorytmów da się w elegancki sposób zapisać w postaci rekurencyjnej  
  * Niestety w niektórych przypadkach (np. ciąg Fibonacciego) otrzymujemy złożoność **wykładniczą**, która nie jest akceptowalna w praktycznych zastosowaniach.

###### Trzy algorytmy obliczające wyraz ciągu Fibonacciego o drastycznie różnych złożon:

**Złożoność wykładnicza** $\displaystyle =\frac1{\sqrt5}\left(\frac{1+\sqrt5}2\right)^n$

```cpp
  int Fib(int n) // O(p^n) 
  {
      if(n>2) 
          return Fib(n-1)+Fib(n-2);
      else 
          return n;
  }
```
**Złożoność liniowa** $=n$

```cpp
  int F(int n) // złożoność O(n)
  {  
     int a=1,b=1;
     for(int i=2; i<n; i++) 
     {
        a=a+b;
        b=a-b;
     } 
     return a;
  }
```
**Złożoność logarytmiczna** = $\log_2n$

>  Złożoność logarytmiczną możemy otrzymać przez mnożenie macierzy z poniższego wzoru, jeśli poprawnie rozwiążemy ostatnie zadanie z  **listy 1**, to znaczy pokażemy, jak potęgować macierze w czasie logarytmicznym:

$$
Fib(n)=\pmatrix{1&0}\pmatrix{1&1\cr 1&0}^{n-1}\pmatrix{1\cr0}
$$

###### Wartości liczbowe typowych złożoności algorytmów dla różnych n

|                          Algorytm                          |   $T(n)$   |  1   |   10   |      n=$100$       |        $10^3$        |      $10^6$       |        $10^9$        |    $10^{12}$    |    $10^{15}$     |
| :--------------------------------------------------------: | :--------: | :--: | :----: | :----------------: | :------------------: | :---------------: | :------------------: | :-------------: | :--------------: |
|      **Wyszukiwanie liniowe**   Fibonacci iteracyjnie      |    $n$     | $1$  |  $10$  |       $100$        |        $10^3$        |      $10^6$       |        $10^9$        |    $10^{12}$    |    $10^{15}$     |
| **Wyszukiwanie binarne** Fibonacci przez mnożenie macierzy | $\log_2 n$ | $0$  | $3.22$ |       $6.64$       |         $10$         |       $20$        |         $30$         |      $40$       |       $50$       |
|                **Czy liczba jest pierwsza**                | $\sqrt n$  | $0$  | $3.16$ |        $10$        |        $31.6$        |      $10^3$       |   $3.16\cdot 10^4$   |     $10^6$      | $3.16\cdot 10^7$ |
|               **Sortowanie przez scalanie**                | $n\log n$  |  1   |  32.2  |        664         |        $10^4$        |   $2\cdot10^7$    |   $3\cdot10^{10}$    | $4\cdot10^{13}$ | $5\cdot10^{16}$  |
|              **Sortowanie przez wstawianie**               |   $n^2$    | $1$  | $100$  |       $10^4$       |        $10^6$        |     $10^{12}$     |      $10^{18}$       |    $10^{24}$    |    $10^{30}$     |
|                **Fibonacci rekurencyjnie**                 |   $p^n$    |  1   |  $55$  | $3.54\cdot10^{20}$ | $4.34\cdot 10^{208}$ | $\sim10^{208987}$ | $\sim10^{208987640}$ |       ...       |       ...        |

**Dla porównania:**

* $1$ minuta $=60s$
* $1$ godzina $=3600s$
* $1$ doba $=8.64\cdot 10^4s$
* $1$ miesiąc $=2.59\cdot 10^6s$
* $1$ rok $=3.15\cdot 10^{7}s$
* $100$ lat $=3.15\cdot 10^{9}s$
* $1000$ lat $=3.15\cdot 10^{10}s$
* Wiek wszechświata $1.4\cdot10^{10}$ lat = $4.4\cdot 10^{20}s$

**Uwaga:** 

  * W niektórych przypadkach,  na przykład w przypadku zrównoważonych drzew binarnych, algorytmy napisane rekurencyjnie mogą być krótkie, przejrzyste i tylko trochę wolniejsze od nierekurencyjnych.
  * Często ładny i zrozumiały algorytm w postaci rekurencyjnej, jest punktem wyjścia do napisania mniej eleganckiej, ale szybszej, wersji nierekurencyjnej.       

## Złożoność algorytmu

Zależy nam na pisaniu szybkich efektywnych algorytmów. Musimy więc umieć ocenić, który algorytm jest lepszy, czyli wykonuje się szybciej i zużywa mniej zasobów.

**Złożoność algorytmu** to zależność ilości zasobów (ilości operacji elementarnych,  ilości pamięci) koniecznych do realizacji algorytmu od rozmiaru problemu.

$T(n)$ - **złożoność czasowa** - ilość operacji elementarnych potrzebnych do wykonania algorytmu na danych $(a_1, ... ,a_n)$


$M(n)$ - **złożoność pamięciowa** - minimalna ilość komórek pamięci gwarantująca poprawne wykonanie algorytmu na danych $(a_1, ... ,a_n)$. Sam rozmiar danych nie jest uwzględniany. $M(n)$ uwzględnia tylko dodatkową pamięć przydzielaną przez algorytm.

## Notacja $o$ - (małe o)

Przy porównywaniu złożoności algorytmów najważniejsze jest ich zachowanie dla dużych $n$ (zachowanie asymptotyczne). 

**Definicja:** Mówimy, że $f(n)$ jest asymptotycznie mniejsza niż $g(n)$ jeśli:
$$
\lim_{n\to\infty} \frac{f(n)}{g(n)}=0
$$
Fakt ten zapisujemy $f(n)=o(g(n))$. 
**Znaczenie praktyczne** - algorytm o złożoności $f(n)$ jest wtedy istotnie szybszy od algorytmu o złożoności $g(n)$, ponieważ proporcja tych czasów dąży do zera wraz ze wzrostem rozmiaru danych do nieskończoności.

**Przykłady:**

* $100n=o(n^2)$ - algorytm o złożoności liniowej jest istotnie szybszy od algorytmu o złożoności kwadratowej.
  
  $$\displaystyle \lim_{n\to\infty}\frac{100n}{n^2}=\lim_{n\to\infty}\frac{100}{n}=0$$
* $\sqrt n=o(n)$ - jeśli przy teście czy liczba jest pierwsza zatrzymamy się na dzielniku $\lfloor\sqrt n\rfloor$ otrzymamy algorytm istotnie szybszy od sprawdzanie wszystkich dzielników od 1 do $n-1$.
  $$\displaystyle \lim_{n\to\infty}\frac{\sqrt{n}}{n}=\lim_{n\to\infty}\frac{1}{\sqrt{n}}=0$$
* $\log n = o(n^\varepsilon)\quad$ jeśli $\varepsilon>0$ - algorytm o złożoności logarytmicznej jest istotnie szybszy od algorytmu $\sqrt[k]{n}$ dla dowolnego $k$.
  
  $$\displaystyle \lim_{n\to\infty}\frac{\log{n}}{n^\varepsilon}=\lim_{n\to\infty}\frac{1/n}{\varepsilon n^{\varepsilon-1}}=\lim_{n\to\infty}\frac{1}{\varepsilon n^{\varepsilon}}=0$$
* $100\cdot n=o(n\log n)$ - algorytm liniowy jest asymptotycznie szybszy od algorytmu klasy $n\log n$

  $$\displaystyle \lim_{n\to\infty}\frac{100\cdot{n}}{n\log n}=\lim_{n\to\infty}\frac{100}{\log n}=0$$

  - w praktyce, ponieważ zazwyczaj rozmiar danych $n$ nie przekracza $2^{64}$, algorytm linowy może być wolniejszy we wszystkich możliwych zastosowaniach, mimo swojej  lepszej asymptotycznej złożoności.

## Notacja $O$ - (duże O)

**Definicja:** Mówimy, że $f(n)$ jest asymptotycznie ograniczona przez $g(n)$ jeśli
istnieje liczba dodatnia $c$ taka, że począwszy od pewnego $n$ zachodzi: $$\displaystyle \frac{f(n)}{g(n)}<c$$  

Taki fakt oznaczamy $f(n)=O(g(n))$ 

**Uwaga:** Znaczy to, że ciąg $$a_n=\frac{f(n)}{g(n)}$$ jest ograniczony z góry.

**Przykłady:**

* $2n=O(n)$ ponieważ: $$ \displaystyle \frac{2n}{n}=2<3$$
* $12 n^2+23n+10^{15}=O(n^2)$ ponieważ: $$\displaystyle \frac{12 n^2+23n+10^{15}}{n^2}<12+23+10^{15}+1$$
* $\log n =O(n^{0,0001})$ ponieważ:  $$ \displaystyle \lim_{n\to\infty}\frac{\log n}{n^k}=0
  \textrm{ więc ciąg } a_n=\frac{\log n}{n^k}\textrm{ jest ograniczony z góry.}$$

## Notacja $\Theta$

**Definicja:** Mówimy, że $f(n)$ i $g(n)$ są asymptotycznie równe, jeśli jednocześnie zachodzą oba warunki
$$
f(n)=O(g(n)) \textrm{ oraz } g(n)=O(f(n))
$$
Jest tak, jeśli istnieją liczby dodatnie $c_1$, $c_2$ takie, że począwszy od pewnego $n$: 
$$
c_1<\frac{f(n)}{g(n)}<c_2
$$

Taki fakt oznaczamy $f(n)=\Theta(g(n))$. Oznacza to, złożoności algorytmów są równe z dokładnością do stałej multiplikatywnej.

**Przykłady:** 

*  $50 n^2-2n+18 =\Theta(n^2)$
  $$
  \frac{50 n^2-2n+18}{n^2}=50 -\frac2n+\frac{18}{n^2}\in(50-2,50+18)
  $$
  
* Gdy $W$ jest  wielomianem stopnia $k$, to  $W(n) = O(n^k)$. Dowód analogiczny.
  
*  Logarytmy dwójkowe i dziesiętne $\log_2 n=\Theta (\log_{10}n)$
  $$
  \frac{\log_2 n}{\log_{10}n}=\log_2 10 \in (3,4)
  $$
  
* $\log_a n=\Theta(\log_b n)$ dla dowolnych $a>b>1$ 

  
  $$
  \frac{\log_a n}{\log_{b}n}=\log_a b \in (\log_a b -1,\log_a b +1)
  $$

  Dlatego często zamiast $\Theta(\log_2 n)$ piszemy $\Theta(\log n)$ pomijając podstawę logarytmu.

*  $\log (n^5+3n+7)=\Theta(\log n)$  
  
  $$
  1<\frac{\log (n^5+3n+7)}{\log n}<\frac{\log (11n^5)}{\log n}<6\quad\textrm{ dla }n>11
  $$
  

**Uwaga:** ze względu na obecność dowolnych stałych $c_1$, $c_2$ w definicji złożoności asymptotycznych $\Theta$, $O$, $o$, zupełnie nieistotna jest jednostka czasu, ani nawet rodzaj komputera na jakim wykonywane są algorytmy. W praktyce przyjmuje się, że ilość **czasu** $T(n)$ potrzebna do wykonania algorytmu jest proporcjonalna do ilości **operacji elementarnych** (np. **mnożeń** lub **porównań**) jakie wykona algorytm. Powoduje to, że najczęściej $T(n)$ wyrażamy za pomocą ilości **operacji elementarnych**.
Jest to wygodne, bo nie zależy od języka programowania, jakości kompilatora, ani szybkości procesora. Czynniki te nie mają wpływu na asymptotyczną złożoność $T(n)$, tylko na wielkość stałych $c_1$ i $c_2$.




# Struktura danych - trzy znaczenia

## 1. Struktura danych - sposób rozmieszania danych w pamięci komputera
**Przykłady:**

* **tablica** - elementy tablicy sąsiadują ze sobą w pamięci. Adres $k$-tego elementu = adres tablicy $+$ $k$. Dostęp do każdego elementu tablicy jest natychmiastowy.
* **lista jednokierunkowa** - znamy adres pierwszego elementu, pierwszy element zawiera klucz i adres następnego elementu, itd.  Aby dostać się do ostatniego elementu, trzeba odwiedzić wszystkie.
* **lista dwukierunkowa** - znamy adres pierwszego i ostatniego elementu. Każdy element zawiera: klucz, adres poprzednika i adres następnika. Można odwiedzać elementy od początku lub od końca.
* **drzewo binarne** - znamy adres korzenia. Korzeń zawiera: klucz, adres lewego poddrzewa, adres prawego poddrzewa. Na $k$-tym poziomie może być $2^k$ węzłów. 
* **drzewo BST** - (binary search tree) drzewo binarne, w którym w lewym poddrzewie są klucze mniejsze, a w prawym większe, niż klucz w ich rodzicu. Umożliwia znalezienie klucza w czasie równym wysokości drzewa. Dla drzew zrównoważonych $\log_2 n$
* **kopiec** - drzewo binarne, w którym klucze dzieci są mniejsze od klucza rodzica. 
  * Kopiec jest często realizowany w tablicy w ten sposób, że element  `t[0]` jest korzeniem kopca  a dziećmi elementu `t[i]` są `t[2i+1]` oraz `t[2i+2]`.
* **tablica list** - $k$-ty element tablicy zawiera adres pierwszego elementu $k$-tej listy. Wykorzystywane w budowaniu tablic z haszowaniem, oraz w algorytmach grafowych - $t[k]$ zawiera wówczas listę krawędzi wychodzących z wierzchołka $k$.
* **macierz** **2D** lub **3D**- tablica tablic lub tablica tablic tablic - element `a[k][j]` zawiera $j$-ty element $k$-tej tablicy. Wykorzystywane np w algorytmach voxelizacji. W trakcie symulacji zderzeń wielu cząstek w 2D lub 3D. Również jako macierze sąsiedztwa a algorytmach grafowych,
* **tablica n-wymiarowa** - tablica tablic (n-1)-wymiarowych. 
* Dowolna kombinacja tych i wielu innych struktur danych.

**Uwaga:** reprezentacja **list** i **drzew** w C++ wymaga dobrej znajomości **wskaźników** oraz operatów **new** oraz **delete**.  Należy powtórzyć sobie wiedzę na ten temat. 

## 2. Struktura danych - zbiór operacji elementarnych do zaimplementowania

**Przykłady:**

* **Stos** (LIFO) (*Push, Pop*)  - ostatni przyszedł, pierwszy wychodzi
* **Kolejka** (FIFO) (*Put, Get*) - pierwszy przyszedł, pierwszy wychodzi
* **Kolejka dwukierunkowa** (deque) (*PushFront, PopFront, PushBack, PopBack*)
* **Kolejka priorytetowa** (*Insert, GetMax*)
* **Struktura zbiorów rozłącznych** (*Union, Find*)
* **Słownik statyczny** (*Find*)
* **Słownik dynamiczny** bez usuwania (*Insert, Find*)  
* **Słownik dynamiczny** (*Insert, Find, Delete*)

## 3. Struktura danych = klasa efektywnie implementująca zadany zbiór operacji. 

Jest to **klasa** (np. w C++), której publiczne **metody** realizują operacje z punktu 2. posługując się zawartymi w części prywatnej strukturami z punktu 1. Przykłady:

* **Stos** (LIFO) zaimplementowany przy użyciu **listy jednokierunkowej**
* **Stos** (LIFO) zrealizowany przy pomocy **tablicy**
* **Słownik** zrealizowany przy użyciu **drzewa BST**, posortowanej **tablicy** lub **tablicy**  z haszowaniem.
* **Kolejka priorytetowa** zrealizowana przy użyciu **kopca**
* Wiele innych. Każda aplikacja definiuje własne potrzeby .

W praktyce wiele języków programowania zawiera biblioteki implementujące powyższe struktury, lub ułatwia ich implementację.

## Wnioski 

*  Dla danego problemu (zbioru operacji elementarnych), należy tak dobrać strukturę danych pomocniczych, i napisać działające na nich algorytmy, by czas ich działania był jak najmniejszy w sensie asymptotycznym.
* Zysk wynikający zastosowania dobrego algorytmu, w porównaniu z niewłaściwym, dla dużych danych, może sięgać wielu rzędów wielkości (np Fibonacci).
* Różnica w prędkości algorytmów dla dużych danych nie jest możliwa do zniwelowania przez nawet bardzo duże inwestycje w zasoby sprzętowe. Superkomputery i klastry realizując gorszy algorytm zostaną w tyle nawet za starym PC.
* Przed implementacją algorytmu warto poszukać literatury, pod kątem najlepszych obecnie znanych algorytmów na rozwiązanie danego problemu.
