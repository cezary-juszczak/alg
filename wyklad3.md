# Sortowanie 

* definicja problemu
* ilość porównań jako miara złożoności: dolne ograniczenie na ilość porównań
* optymalne sortowanie $n$-elementów dla $n=2,3,4,5,6, ..., 10$
* `insertion sort` - sortowanie przez wstawianie: implementacja, złożoność, zastosowania.
* zastosowanie wartownika 
* stabilność sortowania 
* sortowanie bez porównań: `counting sort`, `bucket sort`

## Definicja problemu
Dane $(a_1, ... , a_n)$. Wynik $(b_1, ... ,b_n)$ taki, że:
1. $(b_1, ... ,b_n)$ jest permutacją $(a_1, ... , a_n)$
2. $(b_1, ... ,b_n)$ jest ciągiem niemalejącym: $b_1\leq b_2\leq ...\leq b_n$

## Sortowanie przy pomocy porównań

Dla ciągu różnowartościowego jest tylko jedna permutacja, która spełnia powyższe warunki. 
Natomiast *a piori* każda z $n!$ permutacji jest możliwa.

Używając bisekcji do wybrania jednego elementu z $n!$ możliwych 
wykonamy co najmniej $\log_2(n!)$ porównań.

**Tw. Strilinga** 
$$
 \lim_{n\to \infty} \frac{n!}{(\frac{n}{e})^n\sqrt{2\pi n}}=1
$$

Oznacza to, że 
$$
\log_2(n!)=\log_2\left(\frac{n^n}{e^n}\sqrt{2\pi n}\right)=n\log_2 n-n\log_2e+\frac12 (\log_22\pi+\log_2n)
$$
gdzie dominującym składnikiem jest $n\log_2 n$
### Złożoność 
Zatem pesymistyczna złożoność algorytmu sortującego przy pomocy porównań nie może być lepsza niż:
$$
\log_2(n!)=O(n \log n)
$$
Dowód:
$$
\frac14 n \log n < \frac12 n (\log n - \log 2) =\frac n2 \log \frac n2   = \log \left(\frac n2\right)^{n/2}  < \log n! < \log n^n = n \log n
$$
 gdzie pierwsza nierówność zachodzi dla $n>4$. Więc dla $n>4$
$$
\frac14 n \log n <  \log n! <  n \log n
$$


Powyższe ograniczenie nie dotyczy: 
## Sortowania bez użycia porównań

które jest możliwe, gdy klucze dadzą sie nalezą do zbioru $\{0,... ,m\}$ 
dla niezbyt dużych $m$. Wtedy możemy zrobić sortowanie przez zliczanie:

```cpp
// Idea sortowania przez zliczanie
// to NIE JEST zoptymalizowany algorytm
FIFO<Student> FIFOs[m];
for(auto x:Studenci) 
{
    FIFOs[x.klucz].put(x);
}
int i=0;
for(auto &fifo:FIFOs) 
  while(!fifo.empty())
    Studenci[i++]=fifo.get();
```
Powyższy algorytm daje możliwość wykonania sortowania w czasie liniowym $O(n+m)$.

Jest to możliwe, ponieważ algorytm nie wykonuje porównań (gdzie wynikiem jest wartość TAK/NIE, czyli dwie możliwości) tylko, pobierając klucz (o jednej z $m$ możliwych wartości), posługuje bezpośrednim dostępem do pamięci, by od razu dodać obiekt do właściwej kolejki.


## Insertion sort
jest najprostszym algorytmem sortującym jaki znajduje zastosowanie w praktyce.
W $k$-tym kroku algorytmu $k$ pierwszych elementów tablicy jest już posortowanych i dokładamy do nich kolejny wstawiając go na właściwe miejsce. W tym celu elementy większe od niego przesuwamy o 1 w prawo.

```cpp
void insertion_sort (int n, double t[])
{
    int i;
    for (int k = 1; k < n; k++)
    {   
        double x = t[k]; // x to wstawiany element
        for(i = k; i > 0 && t[i-1] > x; i--)
            t[i] = t[i - 1];
        t[i] = x;
    }
}
```
##### Ulepszenie
Aby w wewnętrznej pętli wyeliminować sprawdzanie, czy $i>0$, można użyć *wartownika*. Jest nim najmniejszy element tablicy, jeśli przeniesie się go na pozycję `t[0]`.

#### Zalety:
* Dla uporządkowanego ciągu wykona tylko $n$ porównań.
* Bardzo szybki dla małych $n$. Mniej więcej dla  $n < 40$.
* Jest to algorytm stabilny: względna kolejność elementów o równych kluczach nie zmienia się.
* Nie zajmuje dodatkowej pomięci - sortuje tablicę *w miejscu*. 

#### Wady:
* W pesymistycznym oraz średnim przypadku wykonuje $O(n^2)$ porównań 
  

#### Porównanie czasu działania insertion_sort z algorytmami klasy $O(n \log n)$

n        |     11 |     44 |    176 |    704 |   2816 |  11264 |  45056 | 180224 | 720896 
:-:        |     :-: |   - |  - |   - |  - |  - | - | - |- 
Quick      |      0 |1.9e-06 |  1e-05 |3.7e-05 |0.00016 |0.00061 | 0.0024 |  0.011 |  0.037 
Merge      |      0 |2.1e-06 |6.9e-06 |4.7e-05 |0.00018 |0.00079 | 0.0034 |  0.014 |  0.061 
Merge-Ins  |      0 |9.5e-07 |  5e-06 |3.1e-05 |0.00014 |0.00066 | 0.0029 |  0.012 |  0.053 
Heap       |9.5e-07 |1.9e-06 |9.1e-06 |4.3e-05 |0.00019 |0.00087 |  0.004 |  0.019 |  0.096 
Insertion  |      0 |1.2e-06 |6.9e-06 |9.5e-05 | 0.0012 |  0.019 |   0.29 |    4.7 |     84 



Widzimy, że dla $n\simeq 10^6$ **sortowanie przez wstawianie** o złożoności $O(n^2)$ jest w praktyce około 1000 razy wolniejsze od algorytmów klasy $O(n\log n$).



