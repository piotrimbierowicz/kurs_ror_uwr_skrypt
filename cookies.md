# Cookies

Cookies to pamięć tymczasowa przeglądarki. Możemy wykorzystać je do zapamiętywania niektórych danych związanych z aplikacją.
Nie jest powiązana z użytkownikiem. Ten sam zalogowany użytkownik będzie miał inne dane w cookies, kiedy korzysta z komputera niż, kiedy korzysta z przeglądarki w telefonie.

Cookies są powiązane z przeglądarką i wysyłaniem zapytań, więc dostępne są tylko w kontrolerach.


### Zapisywanie danych w cookies

```
cookies[:my_key] = '123'
```

Wszystkie dane w cookies przechowywane są jako String!

### Odczytywanie danych z cookies

```
value = cookies[:my_variable]
```


### Podpisywanie cookies

Wartości cookies da się doczytać i zmodyfikować z poziomu przeglądarki, na przykład korzystając z narzedzi deweloperskich chrome. 
Jeśli przechowywane dane są wrażliwe, należy je podpisać.

```
cookies.signed[:my_key] = '123'
```

### Szyfrowane cookies

Jeśli nie chcemy pozwolić użytkownikowi na poznanie wartości cookies, należy je zaszyfrować.

```
cookies.encrypted[:my_key] = '123'
```


Jak użytkownik widzi cookies:

| Sposób zapisania wartości     | Dane przechowywane w przeglądarce                            |
|-------------------------------|--------------------------------------------------------------|
| cookies[:a] = '123'           | 123                                                          |
| cookies.signed[:a] = '123'    | IjEyMyI%3D--e5be76e1ee14421eaac4fdc2b3c4a973e4a61a49         |
| cookies.encrypted[:a] = '123' | Z4vz%2B8U%3D--LCgsXujypebpvVWz--Oc7oA6ux67zffV0V0M97VQ%3D%3D |

Wartość cookie zapisanego metodą signed po zdekodowaniu przy użyciu base64 to `"123"7\n㍵y\ٽ{V`. 

Zatem można łatwo odczytać zapisaną wartość: `'123'`. 

W przypadku metody encrypted nie jest to możliwe.

### Czas życia cookies

Jeśli czas życia cookies nie zostanie podany, wygasają one wraz z zamknięciem przeglądarki.

```
cookies[:a] = { value: '123', expires: 1.hour }

cookies[:b] = { value: '456', expires: Time.utc(2020, 10, 15, 5) }
```


______________

Źródło i więcej informacji: https://api.rubyonrails.org/v5.2.1/classes/ActionDispatch/Cookies.html
