BibliotekaSQL jest relacyjn� baz� danych posiadaj�c� rzeczywiste informacje o stanie ksi��ek b�d�cych w moim posiadaniu. 
Zawiera cztery tabele z informacjami: 
* o autorach (tabela autor), 
* tytu�ach ksia�ek (tabela ksiazka),
* trzeci� (tabela autor_ksiazka) b�d�c� tabel� po�redni�, kt�ra tworzy relacj� wiele-do-wielu pomi�dzy tabelami autor i ksiazka
* a tak�e czwart� (tabela przeczytane) b�d�c� w relacji z tabel� ksi��ka zawieraj�c� list� przeczytanych ksi��ek (info o dacie rozpocz�cia i zako�czenia czytania oraz liczb� stron). 
Warto�ci p�l id_autor oraz id_ksiazka w tabeli autor_ksiazka s� zmi�zane kluczami obcymi z odpowiednimi polami w tabelach autor i ksiazka; podobnie warto�ci z p� id_ksiazka w tabeli przeczytane do klucze obce powi�zane z polami w tabeli ksiazka.

Dane zosta�y odpowiednio przygotowane w Exelu, a nast�pnie przy u�yciu komendy:

INSERT INTO [nazwa tabeli] VALUES ([kolumna1],[kolumna2],...,[kolumnaN])

zaci�gni�te do bazy; nie oby�o si� oczywi�cie bez pomocy komendy

UPDATE [nazwa tabeli] SET [nazwa kolumny] = [warto��] WHERE [warunek]

R�wnie przyjemn�, a mo�e nawet przyjemniejsz� cz�ci�, jest pisanie zapyta� do bazy. Przy tak niewielkiej ilo�ci danych nie s� to jakie� mocno skomplikowane rzeczy, ale mo�na si� ju� pokusi� o JOINy:

implicit JOIN

SELECT a.imie, a.nazwisko, k.tytul
FROM autor AS a, autor_ksiazka AS ak, ksiazka AS k
WHERE a.id_autor = ak.id_autor
AND k.id_ksiazka = ak.id_ksiazka

oraz daj�cy ten sam efekt 

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