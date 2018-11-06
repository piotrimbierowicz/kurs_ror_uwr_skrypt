# Migracje bazy danych

Każda zmiana struktury bazy danych przeprowadzana jest poprzez utworzenie pliku migracji.

Wszystkie migracje przechowywane są w katalogu `db/migrate`.

Wykorzystanie migracji pozwala na zarządzanie i aktualizację bazami danych na wielu komputerach. 
Jest to potrzebne, kiedy wielu programistów pracuje nad jedną aplikacją, a także kiedy aplikacja działa już produkcyjnie z własną bazą danych.

Wyobraźmy sobie następującą sytuację:

1) Programista A zakłada projekt z pustą bazą danych
2) Programista B pobiera projekt i dodaje model User wraz z tabelą w bazie danych
3) Programista A nie pobiera zmian od programisty B, ponieważ te nie są jeszcze gotowe i sam tworzy model Post wraz z tabelą w bazie danych

W kroku 2) i 3) każdy z programistów ma inną strukturę bazy danych. Ich osobiste struktury przechowywane są w pliku `db/schema.rb`

Kiedy zakończą pracę nad swoimi funkcjami, wyślą kod do zdalnego repozytorium. Każdy z nich pobierze zmiany dodane przez kolegę, ale nie chcą utracić zmian wprowadzonych przez siebie.

Gdyby struktura bazy była przechowywana w całości w pliku `db/schema.rb` mogłaby nastąpić utrata części zmian. Zamiast tego w katalogu `db/migrate` widnieją pliki:
- `db/migrate/20181016143022_create_posts.rb`
- `db/migrate/20181023150222_create_users.rb`

Framework pamięta, które pliki migracji zostały już uruchomione na danej maszynie i uruchamiając odpowiednie migracje tak zaktualizuje strukturę bazy, 
a następnie plik `db/schema.rb`, aby obaj programiści mieli tę samą wersję bazy danych.

#### Generowaie pliku migracji

Plik migracji można wygenerować automatycznie (podając parametry takie jak `user_id:integer`):
```
rails g migration add_user_id_to_posts user_id:integer
```

Przy bardziej złożonych migracjach trzeba samodzielnie stworzyć migrację poprzez wygenerowanie pustego pliku:
```
rails g migration rename_columns_in_posts_table
```
i użycie metod modyfikujących strukturę bazy danych.

#### Polecenia

- `rails db:migrate` - wykonuje wszystkie zaległe migracje
- `rails db:rollback` - cofa schemat bazy danych o jedną migrację
- `rails db:migrate:status` - listę migracji wraz ze statusem - czy zostały już załadowane do lokalnej bazy danych


#### Cofanie migracji

Cofanie migracji możliwe jest tylko i wyłącznie jeśli kod nie został jeszcze wysłany do zdalnego repozytorium,

Przykład:
1) Dodajemy migrację
2) Wykonujemy `rails db:migrate`
3) Zauważamy literówkę w migracji
4) Wykonujemy `rails db:rollback`
5) Poprawiamy literówkę w migracji
6) Wykonujemy `rails db:migrate`

Jeśli kod został już wysłany do zdalnego repozytorium, wówczas nie możemy zagwarantować, że po zmigrowaniu bazy danych na wszystkich maszynach ta migracja zostanie cofnięta.

Jeśli błędna migracja została już wysłana:
1) Dodajemy migrację z poprawką, np. `rename_column`
2) Wykonujemy `rails db:migrate`
3) Commitujemy kod i wysyłamy do zdalnego repozytorium


#### Metody dostępne w migracjach

Przykładowe metody:

* `create_table`
* `add_column`
* `rename_column`
* `remove_column`
* `add_index`
* `remove_index`
* `drop_table`

Pełen opis dostępny pod adresem https://api.rubyonrails.org/classes/ActiveRecord/Migration.html


