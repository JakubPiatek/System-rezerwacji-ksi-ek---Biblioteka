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
3. Baza danych: Aplikacja powinna korzystać z wbudowanej bazy danych H2, przechowującej dane w pamięci operacyjnej, które są usuwane po zamknięciu aplikacji.

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
! -- GET /users
```
![image](https://github.com/user-attachments/assets/1d8ee3da-0e99-4a7e-b067-a0a81a96cd2b)

Zwraca listę użytkowników.

```diff
! -- POST /users
```
![image](https://github.com/user-attachments/assets/4e964f6c-dac3-4e75-9c72-8df9862a9ee3)

Dodaje nowego użytkownika do systemu.

```diff
! -- GET /users/{id} (uwzględniając obsługę błędów)
```
![image](https://github.com/user-attachments/assets/99b0f052-5e38-4d03-8de6-f13f697af636)

Informacje o koncie użytkownika o podanym {id}.

![image](https://github.com/user-attachments/assets/82d4b027-5dae-4e94-be9b-11f2ca1710c7)

Nieprawidłowy format ID użytkownika.

![image](https://github.com/user-attachments/assets/d6b28f79-c3e0-4cff-8d11-bf23dcc37f6b)

Użytkownik o podanym ID nie istnieje

```diff
! -- DELETE /users (uwzględniając obsługę błędów)
```
![image](https://github.com/user-attachments/assets/bdd2057e-f8e7-41d2-812f-ce645c7708b1)

Usuwa użytkownika o podanym {id} z systemu.

![image](https://github.com/user-attachments/assets/e177604b-ce5c-4c0c-898f-fe9f18ceb6c2)

Nie można usunąć użytkownika jeśli posiada na koncie nie oddane książki.

![image](https://github.com/user-attachments/assets/2ea8f4f4-8857-49fe-8d3a-f44623e02a4a)

Nieprawidłowy format ID użytkownika.

![image](https://github.com/user-attachments/assets/f65c7052-538f-453d-b76b-7fac8b82a8be)

Użytkownik o podanym ID nie istnieje.

### Przykładowe wyniki dla metod dotyczących zasobu /books, reprezentującego książki
Wyniki testów dla poniższych metod, wraz z omówieniem:
```diff
! -- GET /books?available=false  (uwzględniając filtrowanie)
```
![image](https://github.com/user-attachments/assets/f8b9650b-3f23-4d02-b3a2-9324e6d5de5e)

Zwraca listę wszystkich tytułów książek, jeśli parametr {available} jest ustawiony na false. Parametr {available} jest opcjonalny.

```diff
! -- GET /books?available=true  (uwzględniając filtrowanie)
```
![image](https://github.com/user-attachments/assets/da77ee26-c43f-43e5-812c-988cf0eca13a)

Zwraca listę tytułów książek, których liczba dostępnych egzemplarzy jest większa niż liczba wypożyczonych, jeśli parametr {available} jest ustawiony na true.

```diff
! -- GET /books/{id}  (uwzględniając obsługę błędów)
```
![image](https://github.com/user-attachments/assets/ca6dd3ed-2914-4ff0-bad0-5b9bcd578d32)

Zwraca informacje o wypożyczonych egzemplarzach książki o podanym {id}.

![image](https://github.com/user-attachments/assets/ab8a530b-a2db-47da-9fb5-94a8cb8c87bb)

Nieprawidłowy format ID książki.

![image](https://github.com/user-attachments/assets/41b264ac-6cf1-408a-826f-1de47b3b4b65)

Książka o podanym ID nie istnieje.







