**Tabele złożoności algorytmów sortujących opisanych w książce „Wprowadzenie do algorytmów” (CLRS, wyd. 3)**

W książce Cormena et al. szczegółowo opisane i przeanalizowane są następujące algorytmy sortujące:  
• Sortowanie przez wstawianie (Insertion Sort)  
• Sortowanie przez scalanie (Merge Sort)  
• Sortowanie kopcowe (Heapsort)  
• Sortowanie szybkie (Quicksort – wersja deterministyczna i randomizowana)  
• Sortowanie przez zliczanie (Counting Sort)  
• Sortowanie pozycyjne (Radix Sort)  
• Sortowanie kubełkowe (Bucket Sort)

Poniższa tabela zawiera **złożoność czasową średnią / oczekiwaną** oraz **pesymistyczną (najgorszą)**, a także **złożoność pamięciową (pomocniczą) średnią / oczekiwaną** oraz **pesymistyczną**. Wszystkie wartości podane są w notacji asymptotycznej Θ (lub O tam, gdzie książka podaje luźniejszą granicę).

| Algorytm                        | Czas średni / oczekiwany          | Czas pesymistyczny                | Pamięć średnia / oczekiwana       | Pamięć pesymistyczna              |
|---------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| Sortowanie przez wstawianie     | $\Theta(n^2)$                     | $\Theta(n^2)$                 | $\Theta(1)$                   | $\Theta(1)$                   |
| Sortowanie przez scalanie       | $\Theta(n \lg n)$             | $\Theta(n \lg n)$             | $\Theta(n)$                   | $\Theta(n)$                   |
| Sortowanie kopcowe              | $\Theta(n \lg n)$             | $\Theta(n \lg n)$             | $\Theta(1)$                   | $\Theta(1)$                   |
| Sortowanie szybkie              | $\Theta(n \lg n)$ (oczekiwana dla wersji randomizowanej) | $\Theta(n^2)$ | $\Theta(\lg n)$ (głębokość rekursji) | $\Theta(n)$ (głębokość rekursji) |
| Sortowanie przez zliczanie      | $\Theta(n + k)$               | $\Theta(n + k)$               | $\Theta(n + k)$               | $\Theta(n + k)$               |
| Sortowanie pozycyjne            | $\Theta(d(n + k))$            | $\Theta(d(n + k))$            | $\Theta(n + k)$               | $\Theta(n + k)$               |
| Sortowanie kubełkowe            | $\Theta(n)$¹                  | $\Theta(n^2)$                 | $\Theta(n)$                   | $\Theta(n)$                   |

**Uwagi:**

¹ – średnia złożoność czasowa sortowania kubełkowego jest $\Theta(n)$ **pod warunkiem** jednostajnego rozkładu wartości w przedziale [0, 1) i odpowiedniej liczby kubełków (zgodnie z analizą w rozdziale 8.4 CLRS).  

**Oznaczenia:**  
- $n$ – liczba sortowanych elementów,  
- $k$ – zakres wartości (dla Counting Sort i Radix Sort),  
- $d$ – liczba cyfr (dla Radix Sort),  
- $\lg n = \log_2 n$.

Tabele są zgodne z analizami zamieszczonymi w rozdziałach 2, 6, 7 i 8 książki Cormena. Jeśli potrzebujesz dodatkowej kolumny z najlepszym przypadkiem, przykładów implementacji lub porównania w formie wykresu – daj znać!
