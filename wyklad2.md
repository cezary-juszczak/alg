# Algorytmy i Struktury Danych
## Wykład 2 - rekurencja i drzewa

## Lista jednokierunkowa

$$
L\to\fbox{3}\to\fbox{5}\to\fbox{1}\to\fbox{9}\to\fbox{10}\to{\rm NULL}
$$

Listę jednokierunkową stanowi tak naprawdę dowolny wskaźnik na strukturę `node` i funkcje `insert` i `remove` operujące  na takich wskaźnikach:
```cpp 
struct node
{ 
    int key;    // wartość  użyteczna
    node* next; // wskaźnik na następny węzeł
}; 

void insert(node* &first, int k){ 
    first=new node{k, first};
}

void remove(node* &first){
    node * t=first; 
    first=t->next; 
    delete t;
}
```

Przykład użycia to:
```cpp
int main()
{ 
	node* L=NULL;  // nowa pusta lista

    for(int i=0;i<10;i++) // wkładamy do niej 0,10,20 ...
        insert(L,i*10);   

    while(L){
        cout << L->key << endl;    
        remove(L);  
    }
}
```
Dodawanie elementów na końcu wymaga przejścia przez wszystkie więc zabiera  $O(n)$ czasu. 
```cpp
void insert_at_end(node* &first, int k){ 
	node** t = &first;
	while(*t)	 // dopóki t nie wskazuje na next, który jest nulem
		t = &(**t).next;
    *t = new node(k, mullptr);
}
```
Można to też zrobić rekurencyjnie (niezalecane):
```cpp
void insert_at_end_recursive(node* &first, int k){ 
	if(first == nullptr)
		first = new node(k);
	else
 		insert_at_end_recursive(first->next, k); 
}
```
Złożoności $O(n)$ można uniknąć, jeśli będziemy również pamiętać (i aktualizować) wskaźnik na ostatni element. Żeby to zrobić bezpiecznie najlepiej napisać klasę:
```cpp
// Ćwiczenie dla ciebie

```


## Lista dwukierunkowa
$$
\cdots{\to \atop \leftarrow}\fbox{10}{\to \atop \leftarrow}\fbox{Root}{\to \atop \leftarrow}\fbox{3}{\to \atop \leftarrow}\fbox{5}{\to \atop \leftarrow}\fbox{1}{\to \atop \leftarrow}\fbox{9}{\to \atop \leftarrow}\cdots
$$
Listę dwukierunkową można zaimplementować jako listę kołową z wartownikiem (*sentinel*) do wyeliminowania sytuacji nietypowych. 

Nawet gdy lista jest pusta, to wartownik istnieje. Sam jest wtedy swoim następnikeim i poprzednikiem, co widać już w konstruktorze:
```cpp
deque():root(&root,&root){}
```
Dzięki temu w poniższym kodzie nie ma ani jednej instrukcji `if`:
```cpp
// double ended queue implementation
// by means of 2-linked circular list
// with sentinel

template <class T>
class deque
{
   struct node
   {
      node *prev;
      T key;
      node *next;

      node() : prev(this),next(this) {} // create circular list with one empty element

      node(node *p, T k, node *n) : prev(p), key(k), next(n)
      { // creates new element between p and n
         n->prev = this;
         p->next = this;
      }
      ~node()
      {  // join next with prev omitting this
         prev->next = next; 
         next->prev = prev; 
      }
   };

   node root;

public:
   bool empty() { return root.next == &root; }
   void put_front(T k) { new node(&root, k, root.next); }
   void put_back(T k) { new node(root.prev, k, &root); }
   void pop_front() { delete root.next; }
   void pop_back() { delete root.prev; }
   T front() { return root.next->key; }
   T back() { return root.prev->key; }
   T get_front() { T key = root.next->key; delete root.next; return key; }
   T get_back()  { T key = root.prev->key; delete root.prev; return key; }
   ~deque() { 
      while (root.next != &root) 
      {//  cout<< "usuwam: "<<root.next->key<<endl;
         delete (root.next);
      }
   }
};
```


## Drzewo poszukiwań binarnych


Definicja węzła
```cpp
struct node
{
	int key;               // klucz
	node *left = nullptr;  // zawiera klucze mniejsze od key
	node *right = nullptr; // zawiera klucze nie mniejsze od key

	node(int x0): key(x0){} // konstruktor
};
```
Wstawianie do drzewa (nierekurencyjnie):

```cpp
void insert(node *&t, int x) 
{
	node **t1 = &t;
	while (*t1) // znajdź wskaźnik na null, gdzie można podczepić x
		t1 = &( x < (*t1)->key   // jeśli x < key
				  ? (*t1)->left  // idź w lewo
				  : (*t1)->right // a jak x>=key w prawo
			  );
	*t1 = new node(x); // i go podczep
}
```
Wersja wersja rekurencyjna:
```cpp
void insert_recursive(node *&t, int x) 
{
	if(t == nullptr)                    // jeśli drzewo puste 
		t= new node(x();                // stwórz nowy korzeń zawierający x 
	else if(x < t->key)                 // a jak niepuste i x < key 
	    insert_recursive(t->left, x);   // wstaw x do lewego poddrzewa
	else                                // w przeciwnym wypadku    
		insert_recursive(t->right, x); // wstaw x do prawego poddrzewa
}

```
Wyszukiwanie elementu w drzewie:
```cpp
node *find(node *t, int x) // wyszukiwanie klucza
{
	while (t && t->key != x)
		t = x < t->key
			  ? t->left
			  : t->right;
	return t;
}
```
Wersja rekurencyjna:
```cpp
node *find_recursive(node *t, int x) // wyszukiwanie klucza
{
	if(!t || t->key == x) // jeśli drzewo puste lub klucz jest w korzeniu
	   	return t;         // zwróć korzeń
	if(x<t->key)                           // jeśli x < key  
		return find_recursive(t->left, x);  // znajdź x w lewym poddrzewie
	else                                    // w przeciwnym razie
		return find_recursive(t->right, x); // znajdź x w prawym poddrzewie
}
```
Usuwanie klucza z drzewa binarnego:

* Znajdź węzeł zawierający klucz
* Jeśli ma dwójkę synów:
    * zapamiętaj znaleziony węzeł
    * przejdź jego następnika (minimum w prawym poddrzewie)
    * nadpisz znaleziony wcześniej klucz x kluczem następnika
* teraz jesteś w węźle, który ma co najwyżej jednego syna.
*  usuń ten węzeł a w jego miejsce wstaw syna lub null (jeśli nie ma syna)

```cpp
void remove(node *&t, int x) // usuwanie elementu z drzewa (bez rekurencji)
{
	node **t1 = &t;
	while (*t1 && (*t1)->key != x) // znajdź wskaźnik na węzeł zawierający x
		t1 = x < (*t1)->key
				 ? &(*t1)->left
				 : &(*t1)->right;

	if (*t1) // jeśli znaleziono
	{
		if ((*t1)->right && (*t1)->left) // jeśli ma dwóch synów
		{
			node **t2 = &(*t1)->right; // zaczynając od prawego syna
			while ((*t2)->left)		   // idź w lewo póki można
				t2 = &(*t2)->left;	   // docelowo t2 to minimum prawego poddrzewa
			(*t1)->key = (*t2)->key;   // skopiuj klucz do "usuwanego" węzła
			t1 = t2;				   // i zamiast niego przeznacz ten do usunięcia
		}
		// tutaj *t1 ma już co najwyżej jednego syna
		node *son = (*t1)->right      
				  ? (*t1)->right  // prawy jeśli nie jest pusty
				  : (*t1)->left;  // lewy jeśli prawy pusty
		delete *t1; // usuwamy węzeł
		*t1 = son;	// i zastępujemy synem
	}
}
```



Klucze w drzewie binarnym można wypisywać w rosnąco czyli w porządku "in order". 

```cpp
void inorder(node *t) // wypisanie kluczy w porządku "in order"
{
	if (t)
	{
		inorder(t->left);
		std::cout << t->key << " ";
		inorder(t->right);
	}
}

void prerder(node *t) // wypisanie kluczy w porządku "pre order"
{
	if (t)
	{
		std::cout << t->key << " ";
		prerder(t->left);
		prerder(t->right);
	}
}

void postorder(node *t) // wypisanie kluczy w porządku "post order"
{
	if (t)
	{
		postorder(t->left);
		postorder(t->right);
		std::cout << t->key << " ";
	}
}
```
Ilość kluczy w drzewie i jego wysokość wyznaczamy rekurencyjnie:

```cpp
int n(node *t) // ilość kluczy w drzewie (rekurencyjnie)
{
	return !t ? 0		                 // 0 jeśli drzewo puste
		 : 1 + n(t->left) + n(t->right); // korzeń + lewe + prawe
}

int h(node *t) // wysokość drzewa BST (to samo krócej)
{
	return !t ? 0 					          // 0 jeśli drzewo  puste
		  : 1 + max(h(t->left), h(t->right)); // korzeń + wyższa gałąź

}
```
W drzewie BST aby znaleźć minimum idziemy maksymalnie w lewo:
```cpp

int min(node *t) // minimalny klucz
{
	assert(t);
	while (t->left)
		t = t->left;
	return t->key;
}

int max(node *t) // maksymalny klucz
{
	assert(t);
	while (t->right)
		t = t->right;
	return t->key;
}
```
Zby zwolnić pamięć i usunąć wszystkie klucze z drzewa używamy rekurencji w porządku post order:
```cpp
void destroy(node *&t) // usunięcie drzewa i zwolnienie pamięci (rekurencyjnie)
{
	if (t)                 // jeśli drzewo nie jest puste
	{
		destroy(t->left);  // usuń lewo poddrzewo
		destroy(t->right); // usuń prawe poddrzewo
		delete t;          // usuń korzeń drzewa
		t = nullptr;       // zapisz, że korzeń jest pusty 
	}
}

```

Należy ją wywołać po zakończeniu pracy z drzewem.
