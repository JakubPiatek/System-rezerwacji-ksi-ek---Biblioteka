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
![image](https://github.com/user-attachments/assets/c6870758-a70e-44dc-9ce5-736a260712f2)
![image](https://github.com/user-attachments/assets/06fbfbbe-56a7-4149-bbf3-3bb513545bf8)

Zwraca listę użytkowników.

```diff
! -- POST /users
```
![image](https://github.com/user-attachments/assets/36e7131e-9d11-4674-9ee9-b970fd8dece0)

Dodaje nowego użytkownika do systemu.

```diff
! -- GET /users/{id} (uwzględniając obsługę błędów)
```
![image](https://github.com/user-attachments/assets/ec941067-62e5-4316-b0e2-42e1276bb01b)

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
![image](https://github.com/user-attachments/assets/347f9978-bf5a-4b37-b58b-08c19d1b05a2)
![image](https://github.com/user-attachments/assets/bcfaef51-6e34-4cd0-bc5e-dcf88a6c1251)


Zwraca listę wszystkich tytułów książek, jeśli parametr {available} jest ustawiony na false. Parametr {available} jest opcjonalny.

```diff
! -- GET /books?available=true 
```
![image](https://github.com/user-attachments/assets/a782771b-9104-4157-b709-36d9963844e3)

Zwraca listę tytułów książek, które można wypożyczyć

```diff
! -- GET /books?available=true&author=Mark Lutz
```
Wyszukanie wszystkich książek danego autora, z uwzględniem tytułów książek, które można wypożyczyć

![image](https://github.com/user-attachments/assets/50e74cc1-2149-4e8c-8f5c-c88d2a5e048d)

```diff
! -- GET /books?available=true&author=Mark Lutz&title=Python. Leksykon kieszonkowy
```

![image](https://github.com/user-attachments/assets/0abde2a2-b7b7-4736-b190-4848adfb5712)

Wyszukanie wszystkich książek danego autora, o konkretnym tytule, którą można wypożyczyć.


```diff
! -- GET /books/{id}  (uwzględniając obsługę błędów)
```
![image](https://github.com/user-attachments/assets/ca6dd3ed-2914-4ff0-bad0-5b9bcd578d32)

Zwraca informacje o wypożyczonych egzemplarzach książki o podanym {id}.

![image](https://github.com/user-attachments/assets/ab8a530b-a2db-47da-9fb5-94a8cb8c87bb)

Nieprawidłowy format ID książki.

![image](https://github.com/user-attachments/assets/41b264ac-6cf1-408a-826f-1de47b3b4b65)

Książka o podanym ID nie istnieje.


```diff
! -- POST /books
```

![image](https://github.com/user-attachments/assets/e143a43c-6872-4894-8dca-26a670d259b9)

Dodanie nowej książki do systemu.


```diff
! -- DELETE /books (uwzględniając obsługę błędów)
```
![image](https://github.com/user-attachments/assets/7be5ccf6-8ad0-45da-9f47-1bc6a364a090)

Usuwa książkę o podanym {ID}

![image](https://github.com/user-attachments/assets/f7fe0a29-1631-4595-ae5f-69e3d7a894c8)

Nie można usunąć książki jeśli nie zostały zwrócone wszystkie egzemplarze tej książki

![image](https://github.com/user-attachments/assets/ac8ac17f-a27e-4ba8-b797-4c14dbf1c265)

Nieprawidłowy format ID książki.

![image](https://github.com/user-attachments/assets/09645b40-c3fb-4832-b98b-ecb96fa3e96a)

Książka o podanym ID nie istnieje.

### Przykładowe wyniki dla metod dotyczących zasobu /rents, reprezentującego wypożyczenia
Wyniki testów dla poniższych metod, wraz z omówieniem:

```diff
!-- Get /rents/
```
![image](https://github.com/user-attachments/assets/96e4f292-93c8-4ed6-9e91-470cd1e1539a)

Wyświetl wszystkie wypożyczenia


```diff
!-- Get /rents/{id}
```

![image](https://github.com/user-attachments/assets/e0dadd5e-59cf-4162-a4c6-cd1a72bb7f52)

Wyświetl wypożyczenie o podanym {ID}

![image](https://github.com/user-attachments/assets/a1b4fe12-cae6-45c5-99f6-54b19dc308c3)

Nieprawidłowy format ID wypożyczenia.

![image](https://github.com/user-attachments/assets/4dba91e9-7d44-46e8-97cf-38069a6f5efd)


Wypożyczenie o podanym ID nie istnieje.


```diff
! -- DELETE /rents (uwzględniając obsługę błędów)
```
![image](https://github.com/user-attachments/assets/1b8019ab-6ca1-4f00-b329-3d4cff9ad3dc)

Usuwa wypożyczenie o podanym {ID}

![image](https://github.com/user-attachments/assets/c8e492e4-059a-4204-9a6e-99eff32042e1)

Nie można usunąć wypożyczenia jeśli nie został zwrócony konkretny egzemplarz książki

![image](https://github.com/user-attachments/assets/ff3fe7d2-d02e-4cbe-9502-5885dc73af1b)

Nieprawidłowy format ID wypożyczenia.

![image](https://github.com/user-attachments/assets/057e956c-f503-4031-9e53-873d5d863e0a)

Wypożyczenie o podanym ID nie istnieje.


```diff
!-- PATCH /rents/rent/{id} (uwzględniając obsługę błędów)
```

![image](https://github.com/user-attachments/assets/8dea55cd-4a47-4fe3-b037-27fb96759377)
Wypożyczenie książki o podanym ID przez użytkownika o podanym {ID}.
Książka o ID = 6 została wypożyczona prez użytkownika o ID =  40.


![image](https://github.com/user-attachments/assets/0e90332d-66ba-41a7-9fdc-615e99056c00)

Nie ma dostępnych wolnych egzemplarzy dla podanego identyfikatora książki


![image](https://github.com/user-attachments/assets/914cbc6f-2cfb-422d-ad11-2ecc0863cade)

![image](https://github.com/user-attachments/assets/1316ceb4-fc1a-4299-9866-e018fce837b1)

Podany identyfikator książki nie istnieje lub jest nieprawidłowy

![image](https://github.com/user-attachments/assets/406e95ba-084a-4574-90bb-f6ba70ac1f2d)
![image](https://github.com/user-attachments/assets/992f9355-59e8-41b9-9cda-a78d9cdacdfb)

Podany identyfikator użytkownika nie istnieje lub jest nieprawidłowy


```diff
! -- PATCH /rents/return/{id}  
```

![image](https://github.com/user-attachments/assets/c01150b9-979b-4b78-9e5e-045082586002)

Zwrot wypożyczonego egzemplarza książki o podanym {ID} przez konretnego użytkownika.
ID użytkownika podane w (header)


![image](https://github.com/user-attachments/assets/cbac5572-07e9-40db-ad10-344554789e96)

Nie ma możliwośći zwrotu książki, którą użytkownik już wcześniej zwrócił


![image](https://github.com/user-attachments/assets/6b902e1f-99f6-4f87-b86b-7d0af3c708a6)
![image](https://github.com/user-attachments/assets/9f54cdf8-c2c3-4e86-ad5e-d21f3cfa9dd9)

Możliwość zwrotu i wypożyczenia tej samej książki 


![image](https://github.com/user-attachments/assets/98c33108-9c70-4de9-90a9-156cafc09b1f)

![image](https://github.com/user-attachments/assets/fd7e987f-6e67-4900-93f6-411d39da4d8d)

Podany identyfikator książki nie istnieje lub jest nieprawidłowy

![image](https://github.com/user-attachments/assets/97bcde76-cb8b-49bd-8018-51408588563b)
![Uploading image.png…]()

Podany identyfikator użytkownika nie istnieje lub jest nieprawidłowy









