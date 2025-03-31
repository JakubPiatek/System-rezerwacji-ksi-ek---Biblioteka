# System Rezerwacji Książek - Biblioteka

Celem Projektu jest utworzenie monolitycznej aplikacji udostępniającej interfejs REST w oparciu o Spring Boot i język Java.

## Przygotowanie Środowiska
Aby rozpocząć pracę z projektem, należy zainstalować odpowiednie oprogramowanie:
- Instalacja IntelliJ IDEA - Popularne IDE do pracy z Javą.
- Instalacja Java SE 21 - Wymagana wersja Javy do uruchomienia projektu.
- Instalacja Postman - narzędzia do testowania poprawności działania aplikacji.

## Wymagania dotyczące aplikacji
1. Dostęp do systemu: Nie wymaga autoryzacji.
2. Adres dostępności: Po uruchomieniu aplikacji zasoby powinny być dostępne pod adresem: http://localhost:8080.
3. Zasoby i funkcjonalności: Udostępniane przez REST API zgodne z dokumentacją zawartą w pliku library-rest-service.yaml.
4. Baza danych: Aplikacja powinna wykorzystywać wbudowaną bazę danych H2 do przechowywania stanu systemu.


## Instalacja
Projekt został wygenerowany za pomocą Spring Initializr[https://start.spring.io] projekt startowy dla języka Java 21 oparty o narzędzie Maven. Wymagania do projektu:
> * Metoda dystrybucji: **JAR**
> * Dane projektu:
>    * Grupa: **com.portfolio**
>    * Artefakt i nazwa: **library-monolith**
>    * Opis: **Aplikacja typu monolit do obsługi biblioteki**
>    * Nazwa paczki: **com.portfolio.library_monolith**
> * Wersja Spring Boot: **3.3.10**
> * Wymagane zależności:
>    * Spring Web
>    * Baza danych H2
>    * Moduł Flyway
>    * JDBC API

## Uruchomienie projektu 
Po pobraniu projektu uruchom aplikację za pomocą:

![image](https://github.com/user-attachments/assets/5e810cbf-e152-4c9c-b9f1-475eb513ce98)

## Bazy danych H2

### Diagram ERD bazy danych
![image](https://github.com/user-attachments/assets/c54c2297-46c3-4c5a-96c6-8b251d07d78f)

### Plik SQL z zapisanymi rekordami do bazy danych 
![image](https://github.com/user-attachments/assets/d5be4589-8f55-4e4f-a894-89dcc401f8aa)

### Konfiguracja połączenia do bazy danych H2 została zapisana w pliku `application.properties`:
```ini
   spring.datasource.url=jdbc:h2:mem:librarydb
   spring.datasource.driverClassName=org.h2.Driver
   spring.datasource.username=admin
   spring.datasource.password=password
   spring.h2.console.enabled=true
```
### Po uruchomieniu aplikacji dostęp do konsoli H2 w przeglądarce jest możliwy po wpisaniu odpowiedniego adresu URL:
```bash
http://localhost:8080/h2-console/
```
### Tabela `users`
#### Tabela `users` przechowuje informacje o użytkownikach systemu bibliotecznego. Każdy rekord w tabeli reprezentuje jednego użytkownika i zawiera następujące pola:
> * ID – Unikalny identyfikator użytkownika.
> * NAME – Imię i nazwisko użytkownika.
> * ROLES – Role przypisane do użytkownika (np. user, admin), określające jego uprawnienia w systemie.

![image](https://github.com/user-attachments/assets/0b82a8ab-fe1d-4d52-a21a-799eadf7732f)

### Tabela `books`
#### Tabela `books` przechowuje informacje o książkach dostępnych w bibliotece. Każdy rekord w tabeli reprezentuje jedną książkę i zawiera następujące pola:
> * ID – Unikalny identyfikator książki.
> * TITLE – Tytuł książki.
> * AUTHOR – Autor książki.
> * QUANTITY - Całkowita liczba egzemplarzy danej książki dostępnych w bibliotece (niezależnie od aktualnej liczby wypożyczonych egzemplarzy).

![image](https://github.com/user-attachments/assets/5885276f-124f-4a7a-acab-f8045a3df9cd)

### Tabela `rentals`
#### Tabela `rentals` przechowuje informacje o wypożyczeniach książek przez użytkowników. Każdy rekord w tabeli reprezentuje jedno wypożyczenie książki i zawiera następujące pola:
> * ID – Unikalny identyfikator wypożyczenia.
> * USERID_FK – Identyfikator użytkownika, który wypożyczył książkę (klucz obcy powiązany z tabelą users).
> * BOOKID_FK – Identyfikator książki, która została wypożyczona (klucz obcy powiązany z tabelą books).
> * RENTAL_DATE - Data wypożyczenia książki. 
> * RETURN_DATE - Data zwrócenia książki.

![image](https://github.com/user-attachments/assets/dc87e579-2855-4ae1-a84b-08ff8d4bcfae)

## Funkcje systemu
### Przykładowe wyniki dla metod dotyczących zasobu /users, reprezentującego użytkowników
Wyniki testów dla poniższych metod, wraz z omówieniem:
```diff
! -- GET /users (uwzględniając obsługę błędów)
```
![image](https://github.com/user-attachments/assets/1d8ee3da-0e99-4a7e-b067-a0a81a96cd2b)

Zwrócenie listy wszystkich użytkowników.




! -- DELETE /users (uwzględniając obsługę błędów)
! -- POST /users
! -- GET /books (uwzględniając filtrowanie)
! -- PATCH /books/return lub PATCH /books/rent (uwzględniając obsługę błędów)
```

System rezerwacji książek w bibliotece umożliwia

5. Wyniki testów dla następujących metod wraz z omówieniem dołącz do sprawozdania.
Uzytkownicy:
GET /users


![image](https://github.com/user-attachments/assets/1d8ee3da-0e99-4a7e-b067-a0a81a96cd2b)

GET /users/{id} (uwzględniając obsługę błędów)

![image](https://github.com/user-attachments/assets/a9d84913-105c-4dca-983a-f54eabe8b33b)


DELETE /users/{id} (uwzględniając obsługę błędów)

![image](https://github.com/user-attachments/assets/57e0486c-24c9-4f34-94a4-0b4364b77570)

Nie można usunąć użytkownika, który ma wypożyczoną książkę

![image](https://github.com/user-attachments/assets/4d085ae7-f96e-4006-86a0-f31a189d6f56)

POST /users


![image](https://github.com/user-attachments/assets/9015b0c1-ab1b-46de-8ff8-a9a359de3941)


![image](https://github.com/user-attachments/assets/81c98089-0130-4e6f-b1bb-133d1c5ad835)

Ksiazki:
GET /books (uwzględniając filtrowanie)


![image](https://github.com/user-attachments/assets/b1daf11e-9be2-4981-895d-0a7e8b289377)
Pobranie listy dostępnych książek (liczba dostępnych egzemplarzy większa niż liczba wypożyczonych)


![image](https://github.com/user-attachments/assets/347a7f6b-daae-4c01-a394-8da329fadb53)

GET /books/{id}(uwzględniając obsługę błędów)
Zwraca informacje na temat wypożyczonych egzemplarzy dla tytułu o podanym {id}


![image](https://github.com/user-attachments/assets/8176f277-01ab-4009-b809-28a1a39b72ec)

## Zasoby i funkcjonalność są udostępniane przez REST API zgodne z dokumentacją zawartą w pliku library-rest-service.yaml.

![image](https://github.com/user-attachments/assets/8da9bce7-7c87-41d3-8f49-d56a19d07aad)

## Wyniki testów dla następujących metod wraz z omówieniem dołącz do sprawozdania.
### Uzytkownicy:
GET /users



System rezerwacji książek w bibliotece umożliwia:

- Pobieranie listy użytkowników, dodawanie nowych oraz usuwanie istniejących

- Pobieranie listy dostępnych książek
- 
- obieranie informacji o konkretnej książce wraz z jej historią wypożyczeń

- Wypożyczanie oraz zwracanie książek przez użytkowników


System powinien umożliwiać:
pobranie listy użytkowników, usuwanie oraz dodawanie nowych użytkowników,
pobranie listy dostępnych książek,
pobranie informacji o książce wraz z jej historią wypożyczeń,
wypożyczenie oraz zwrot książki przez użytkownika.





5. Wyniki testów dla następujących metod wraz z omówieniem dołącz do sprawozdania.
Uzytkownicy:
GET /users


![image](https://github.com/user-attachments/assets/1d8ee3da-0e99-4a7e-b067-a0a81a96cd2b)

GET /users/{id} (uwzględniając obsługę błędów)

![image](https://github.com/user-attachments/assets/a9d84913-105c-4dca-983a-f54eabe8b33b)


DELETE /users/{id} (uwzględniając obsługę błędów)

![image](https://github.com/user-attachments/assets/57e0486c-24c9-4f34-94a4-0b4364b77570)

Nie można usunąć użytkownika, który ma wypożyczoną książkę

![image](https://github.com/user-attachments/assets/4d085ae7-f96e-4006-86a0-f31a189d6f56)

POST /users


![image](https://github.com/user-attachments/assets/9015b0c1-ab1b-46de-8ff8-a9a359de3941)


![image](https://github.com/user-attachments/assets/81c98089-0130-4e6f-b1bb-133d1c5ad835)

Ksiazki:
GET /books (uwzględniając filtrowanie)


![image](https://github.com/user-attachments/assets/b1daf11e-9be2-4981-895d-0a7e8b289377)
Pobranie listy dostępnych książek (liczba dostępnych egzemplarzy większa niż liczba wypożyczonych)


![image](https://github.com/user-attachments/assets/347a7f6b-daae-4c01-a394-8da329fadb53)

GET /books/{id}(uwzględniając obsługę błędów)
Zwraca informacje na temat wypożyczonych egzemplarzy dla tytułu o podanym {id}


![image](https://github.com/user-attachments/assets/8176f277-01ab-4009-b809-28a1a39b72ec)













