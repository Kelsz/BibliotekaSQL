BibliotekaSQL jest relacyjn¹ baz¹ danych posiadaj¹c¹ rzeczywiste informacje o stanie ksi¹¿ek bêd¹cych w moim posiadaniu. 
Zawiera cztery tabele z informacjami: 
* o autorach (tabela autor), 
* tytu³ach ksia¿ek (tabela ksiazka),
* trzeci¹ (tabela autor_ksiazka) bêd¹c¹ tabel¹ poœredni¹, która tworzy relacjê wiele-do-wielu pomiêdzy tabelami autor i ksiazka
* a tak¿e czwart¹ (tabela przeczytane) bêd¹c¹ w relacji z tabel¹ ksi¹¿ka zawieraj¹c¹ listê przeczytanych ksi¹¿ek (info o dacie rozpoczêcia i zakoñczenia czytania oraz liczbê stron). 
Wartoœci pól id_autor oraz id_ksiazka w tabeli autor_ksiazka s¹ zmi¹zane kluczami obcymi z odpowiednimi polami w tabelach autor i ksiazka; podobnie wartoœci z pó³ id_ksiazka w tabeli przeczytane do klucze obce powi¹zane z polami w tabeli ksiazka.

Dane zosta³y odpowiednio przygotowane w Exelu, a nastêpnie przy u¿yciu komendy:

INSERT INTO [nazwa tabeli] VALUES ([kolumna1],[kolumna2],...,[kolumnaN])

zaci¹gniête do bazy; nie oby³o siê oczywiœcie bez pomocy komendy

UPDATE [nazwa tabeli] SET [nazwa kolumny] = [wartoœæ] WHERE [warunek]

Równie przyjemn¹, a mo¿e nawet przyjemniejsz¹ czêœci¹, jest pisanie zapytañ do bazy. Przy tak niewielkiej iloœci danych nie s¹ to jakieœ mocno skomplikowane rzeczy, ale mo¿na siê ju¿ pokusiæ o JOINy:

implicit JOIN

SELECT a.imie, a.nazwisko, k.tytul
FROM autor AS a, autor_ksiazka AS ak, ksiazka AS k
WHERE a.id_autor = ak.id_autor
AND k.id_ksiazka = ak.id_ksiazka

oraz daj¹cy ten sam efekt 

explicit JOIN

SELECT imie, nazwisko, tytul
FROM autor INNER JOIN autor_ksiazka
ON autor.id_autor = autor_ksiazka.id_autor INNER JOIN ksiazka
ON autor_ksiazka.id_ksiazka = ksiazka.id_ksiazka

lub

SELECT imie, nazwisko, tytul
FROM autor INNER JOIN autor_ksiazka
USING (id_autor) INNER JOIN ksiazka
USING (id_ksiazka)