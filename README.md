<<<<<<< HEAD
# L03: Zaawansowane techniki programowania

Celem zadania będzie przygotowanie monolitycznej aplikacji udostępniającej prosty interfejs REST w oparciu o Spring Boot i język Java.

## Przygotowanie

Przed zajęciami proszę o zapoznanie się z [załączonymi materiałami](docs/introduction.md) oraz o zainstalowanie niezbędnego oprogramowania, które będzie wykorzystywane na tych i kolejnych zajęciach.
W przypadku braku znajomości języka SQL polecam zapoznanie się z [dodatkowymi materiałami pomocniczymi](docs/sql_cheetsheet.md) wymaganymi do realizacji komunikacji z bazą danych.

## Wymagania dotyczące aplikacji

1. Dostęp do aplikacji nie powinien wymagać autoryzacji, a po uruchomieniu aplikacji wszystkie zasoby powinny być dostępne pod adresem [http://localhost:8080](http://localhost:8080).
1. Zasoby i funkcjonalność powinny być udostępniane przez REST API zgodne z dokumentacją zawartą w [docs/library-rest-service.yaml](https://epam-online-courses.github.io/ZTP-Java-REST-Monolith/).
1. Aplikacja powinna wykorzystywać wbudowaną bazę danych H2 do przechowywania stanu systemu.

## Kryterium oceny rozwiązania
```diff
! Za poprawne rozwiązania zadania można otrzymać 5 punktów.
```
**1. Zgodność oraz poprawność implementacji funkcjonalności opisanej w ramach REST API**
> Aplikacja powinna umożliwiać:
> * pobranie listy użytkowników, usuwanie oraz dodawanie nowych użytkowników,
> * pobranie listy dostępnych książek,
> * pobranie informacji o książce wraz z jej historią wypożyczeń
> * wypożyczenie oraz zwrot książki przez użytkownika
>
> Proszę zwrócić szczególną uwagę na trzymanie się formatu danych (JSON) oraz obsługi błędów zdefiniowanych w ramach dokumentacji [REST API](https://epam-online-courses.github.io/ZTP-Java-REST-Monolith/).
> Dodatkowa funkcjonalność nie wymagana w ramach zadania nie będzie wypływała na ocenę końcową.

**2. Sprawozdanie z laboratorium**
> Dołączenie sprawozdania do zrealizowanego zdania jest warunkiem koniecznym do uzyskania pozytywnej oceny z laboratorium. Zadania bez sprawozdania lub ze sprawozdaniem zawierającym znaczące braki merytoryczne nie będą podlegały ocenie.
>
> Sprawozdanie powinno zostać zamieszczone w katalogu [docs](docs) i dodane do repozytorium w oddzielnym commicie pod tytułem "**Sprawozdanie**".

**3. Termin dostarczenia rozwiązania**
> Bezpośrednio po zajęciach w repozytorium powinny znaleźć się wynik prac zakończonych w trakcie laboratorium.
>
> Ostatecznym terminem na wysłanie rozwiązania zadania wraz ze sprawozdaniem jest **14.11.2021 23:59** (decyduje data ostatniego commitu).
>
> Ocena za zadania dostarczone po tym terminie będzie automatycznie obniżana o 1 punkt, natomiast zadania nadesłane po **21.11.2021 23:59** nie będą podlegały ocenie.

## Zadania do wykonania w ramach laboratorium

### Krok 1
Wykonaj lokalną kopię prywatnego repozytorium z zadaniem dostępnego na platformie GitHub Classroom.

### Krok 2
Wygeneruj za pomocą [https://start.spring.io](https://start.spring.io) projekt startowy dla języka Java 11 oparty o narzędzie Maven. Wymagania do projektu:
> * Metoda dystrybucji: **JAR**
> * Dane projektu:
>    * Grupa: **pl.edu.pk.ztp**
>    * Artefakt i nazwa: **library-monolith**
>    * Opis: **Aplikacja typu monolit do obsługi biblioteki**
>    * Nazwa paczki: **pl.edu.pk.ztp.library-monolith**
> * Wersja Spring Boot: **2.5.6**
> * Wymagane zależności:
>    * Spring Web
>    * Baza danych H2
>    * Moduł Flyway
>    * JDBC API

### Krok 3
Pobrany szablon projektu rozpakuj do katalogu głównego repozytorium tak, aby katalog `src` z archiwum znajdował się w bezpośrednio w katalogu głównym repozytorium.
```diff
! Wykonaj zrzut ekranu struktury projektu po zaimportowaniu do IDE i dołącz do sprawozdania.
```
### Krok 4
Zaktualizuj konfigurację projektu w IDE tak, aby był on rozpoznawany jako projekt Mavenowy, a następnie uruchom aplikację.
```diff
! Wynik uruchomienia dołącz do sprawozdania wraz z komentarzem wyjaśniającym 
! poszczególne etapy inicjalizacji aplikacji oraz źródło błędu.
```
### Krok 5
Zaktualizuj konfigurację połączenia do bazy danych H2 zapisaną w pliku `application.properties` zgodnie z wymaganiami poniżej:
```ini
   spring.datasource.url=jdbc:h2:mem:librarydb
   spring.datasource.driverClassName=org.h2.Driver
   spring.datasource.username=admin
   spring.datasource.password=password
   spring.h2.console.enabled=true
```
```diff
! W ramach sprawozdania wyjaśnij znaczenie poszczególnych opcji konfiguracyjnych.
```
### Krok 6
Przenieś plik odpowiedzialny za inicjalizację bazy danych `V1_0__create_librarydb_schema.sql` z katalogu [docs](src/main/resources/db/migration/V1_0__create_librarydb_schema.sql) do `resources/db/migration` oraz uruchom aplikację ponownie.
```diff
! Wynik uruchomienia dołącz do sprawozdania wraz z komentarzem 
! wyjaśniającym poszczególne etapy inicjalizacji aplikacji.
```
### Krok 7
Dodaj do aplikacji klasy odpowiedzialne za reprezentacje danych w formacie JSON zgodnie z dokumentacją zamieszczoną w [docs/library-rest-service.yaml](https://epam-online-courses.github.io/ZTP-Java-REST-Monolith/).
* `pl.edu.pk.ztp.librarymonolith.dto.UserDTO` reprezentacja modelu **User**
* `pl.edu.pk.ztp.librarymonolith.dto.BookDTO` reprezentacja modelu **Book**
* `pl.edu.pk.ztp.librarymonolith.dto.BookRentalDTO` reprezentacja modelu **BookRental**
```diff
! W ramach sprawozdania wyjaśnij kluczowe adnotacje wykorzystane 
! do konfiguracji procesu serializacji do formatu JSON.
```
### Krok 8
Dodaj do aplikacji klasę repozytorium odpowiedzialną za udostępnianie danych zapisanych w bazie danych w tabeli `tbl_users`. 
Klasa powinna posiadać następującą nazwę `pl.edu.pk.ztp.librarymonolith.repository.UserRepository` oraz udostępniać następujące metody publiczne:
* `List<UserDTO> findAll()`
* `UserDTO findByUserId(final Integer userID)`
* `boolean deleteUserById(final Integer userID)`
* `UserDTO createUser(final UserDTO user)`
```diff
! W ramach sprawozdania wyjaśnij cel oraz działanie zastosowanych 
! w ramach tej klasy adnotacji @Repository oraz @Autowired
```
### Krok 9
Dodaj do aplikacji klasę `pl.edu.pk.ztp.librarymonolith.rest.UsersController` odpowiedzialną za obsługę zasobu `/users` zgodnie z dokumentacją zamieszczoną w [docs/library-rest-service.yaml](https://epam-online-courses.github.io/ZTP-Java-REST-Monolith/).
Klasa powinna udostępniać następujące metody publiczne:
* `List<UserDTO> getAllUsers()`
* `UserDTO getUserById(final Integer userID)`
* `void deleteUser(final Integer userID)`
* `UserDTO postUser(final UserDTO user)`
```diff
! W ramach sprawozdania wyjaśnij kluczowe elementy wykorzystane do konfiguracji zasobu 
! zgodnie z dokumentacją oraz sposób w jaki rozwiązana została obsługa błędów.
```
### Krok 10
Dodaj do aplikacji klasę repozytorium odpowiedzialną za udostępnianie danych zapisanych w bazie danych w tabeli `tbl_books` oraz `tbl_rentals`. Klasa powinna posiadać następującą nazwę `pl.edu.pk.ztp.librarymonolith.repository.BookRepository`
```diff
! W ramach sprawozdania udokumentuj publiczne metody zdefiniowane w ramach tej klasy.
! Opis powinien zawierać sygnaturę metody oraz krótki opis jej działania.
``` 
### Krok 11
Dodaj do aplikacji klasę `pl.edu.pk.ztp.librarymonolith.rest.BooksController` odpowiedzialną za obsługę zasobu `/books` zgodnie z dokumentacją zamieszczoną w  [docs/library-rest-service.yaml](https://epam-online-courses.github.io/ZTP-Java-REST-Monolith/).
Klasa powinna udostępniać następujące metody publiczne:
* `List<BookDTO> getAllBooks(final boolean showOnlyAvailable)`
* `BookDTO getBookRentals(final Integer bookID)`
* `BookDTO patchRentBook(final Integer bookID, final Integer userID)`
* `BookDTO patchReturnBook(final Integer bookID, final Integer userID)`
```diff
! W ramach sprawozdania wyjaśnij kluczowe elementy wykorzystane do konfiguracji zasobu 
! zgodnie z dokumentacją oraz sposób w jaki rozwiązana została obsługa błędów.
```
### Krok 12
Przetestuj poprawność działania aplikacji za pomocą narzędzia Postman lub dowolnego innego narzędzia.
* Przykładowe pliki testów dla zasobu `/users` znajdują się w pliku [docs/postman_test_users.json](docs/postman_test_users.json)
* Przykładowe pliki testów dla zasobu `/books` znajdują się w pliku [docs/postman_test_books.json](docs/postman_test_books.json)
```diff
! Wyniki testów dla następujących metod wraz z omówieniem dołącz do sprawozdania.
! -- GET /users (uwzględniając obsługę błędów)
! -- DELETE /users (uwzględniając obsługę błędów)
! -- POST /users
! -- GET /books (uwzględniając filtrowanie)
! -- PATCH /books/return lub PATCH /books/rent (uwzględniając obsługę błędów)
```
=======
# System Rezerwacji Książek - Biblioteka

System rezerwacji książek w bibliotece umożliwia:

- Pobieranie listy użytkowników, dodawanie nowych oraz usuwanie istniejących

- Pobieranie listy dostępnych książek
- 
- obieranie informacji o konkretnej książce wraz z jej historią wypożyczeń

- Wypożyczanie oraz zwracanie książek przez użytkowników

## Instalacja

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install foobar.

bash
pip install foobar


## Usage

python
import foobar

# returns 'words'
foobar.pluralize('word')

# returns 'geese'
foobar.pluralize('goose')

# returns 'phenomenon'
foobar.singularize('phenomena')


## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/) na podstawie tego zrób powyższ y opis


System powinien umożliwiać:
pobranie listy użytkowników, usuwanie oraz dodawanie nowych użytkowników,
pobranie listy dostępnych książek,
pobranie informacji o książce wraz z jej historią wypożyczeń,
wypożyczenie oraz zwrot książki przez użytkownika.

1. Projekt wygenerowany za pomocą https://start.spring.io projekt startowy dla języka Java oparty o narzędzie Maven.
Wymagania do projektu:
Wersja Spring Boot: 3.3.10,
Java: 21.
Wymagane Zależności:
Spring Web,
Baza danych H2,
Moduł Flyway,
JDBC API

2. Uruchomienie Systemu

![image](https://github.com/user-attachments/assets/5e810cbf-e152-4c9c-b9f1-475eb513ce98)

3. Baza danych H2
   
Tabela bazy danych
![image](https://github.com/user-attachments/assets/c54e7a59-fa79-41d4-95e6-1af0c1c6a898)

Plik sql z zapisanym rekordami do bazy danych 
![image](https://github.com/user-attachments/assets/d5be4589-8f55-4e4f-a894-89dcc401f8aa)

Połączenie do bazy danych
![image](https://github.com/user-attachments/assets/753b2ed1-fd74-4137-8546-8f98b802d078)

Możliwość wykonywania zapytań w przeglądarce po uruchomieniu aplikacji: 
Po wpisaniu adresu ur
![image](https://github.com/user-attachments/assets/6001ca88-929f-44e1-b33d-29615d532d50)

Tabela użytkowników


![image](https://github.com/user-attachments/assets/b23ce30a-5152-444e-bb24-c768c83ba5d9)

Tabela książek


![image](https://github.com/user-attachments/assets/abf9dda4-e16d-4ece-b35a-9632d43b09e7)


Tabela wypożyczeń

![image](https://github.com/user-attachments/assets/60d177bb-26e2-4145-ae6a-b832c66b7744)

4. Wymagania dotyczące aplikacji
Dostęp do aplikacji nie powinien wymagać autoryzacji, a po uruchomieniu aplikacji wszystkie zasoby powinny być dostępne pod adresem http://localhost:8080.

Zasoby i funkcjonalność są udostępniane przez REST API zgodne z dokumentacją zawartą w pliku library-rest-service.yaml.

![image](https://github.com/user-attachments/assets/8da9bce7-7c87-41d3-8f49-d56a19d07aad)

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









>>>>>>> 917c82b00633293fff574d9d8d645dd7f2077812




