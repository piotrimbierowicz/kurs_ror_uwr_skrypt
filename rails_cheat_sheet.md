# Rails cheat sheet

W tym dokumencie można znaleźć komendy i fragmenty kodu przydatne przy rozwijaniu aplikacji napisanej w Ruby on Rails.

## Sprawdzenie wersji rails - `rails -v`

Przed utworzeniem nowego projektu należy sprawdzić jaka wersja Rails jest aktualnie wykorzystywana przez system.

Utworzenie projektu z wykorzystaniem starej lub nieodpowiedniej wersji Rails może skutkować koniecznością wykonania aktualizacji ręcznie.

Przy rozpoczynaniu nowego projektu warto skorzystać z najnowszej stablilnej wersji.

## Tworzenie nowego projektu - `rails new APP_PATH [options]`

Aby sprawdzić dostępne opcje należy wpisać `rails new --help`

#### Parametr `APP_PATH`

`APP_PATH` to katalog dla aplikacji i jednocześnie jej nazwa (namespace). 

Przykładowo `rails new my_blog` utworzy aplikację `MyBlog::Application` w katalogu `/my_blog`. 

#### Dodatkowe opcje (przykładowe)

* `--skip-turbolinks`
* `--database=postgresql`
* `--skip-test`
 
## Migracje bazy danych

Pełny dokument o migracjach - [migrations.md](migrations.md)

Wszystkie migracje przechowywane są w katalogu `db/migrate`.
Aktualny schemat bazy danych przechowywany jest w `db/schema.rb`.

#### Polecenia

- `rails db:migrate` - wykonuje wszystkie zaległe migracje
- `rails db:rollback` - cofa schemat bazy danych o jedną migrację
- `rails db:migrate:status` - listę migracji wraz ze statusem - czy zostały już załadowane do lokalnej bazy danych
