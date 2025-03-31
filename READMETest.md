# System Rezerwacji Książek - Biblioteka

Celem Projektu jest utworzenie monolitycznej aplikacji udostępniającej interfejs REST w oparciu o Spring Boot i język Java.

## Przygotowanie Środowiska
Aby rozpocząć pracę z projektem, należy zainstalować odpowiednie oprogramowanie:
- Instalacja IntelliJ IDEA - Popularne IDE do pracy z Javą.
- Instalacja Java SE 21 - Wymagana wersja Javy do uruchomienia projektu.

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

# Tabela bazy danych H2

## Diagram ERD bazy danych
![image](https://github.com/user-attachments/assets/c54c2297-46c3-4c5a-96c6-8b251d07d78f)


Możliwość wykonywania zapytań w przeglądarce po uruchomieniu aplikacji: 
Po wpisaniu adresu url:
```bash
http://localhost:8080/h2-console/
```
## Tabela `users`: Przechowuję dane użytkowników systemu. Zawiera informacje o identyfikatorze użytkownika (ID), nazwię użytkownika oraz przypisanych rolach. 

![image](https://github.com/user-attachments/assets/7fdd359c-5099-4cd9-b515-ea3c11967272)


## Tabela `books`: Przechowuje informacje o książkach dostępnych w bazie danych. Zawiera dane takie jak identyfikator książki (ID), tytuł, autora oraz liczbę wszystkich egzemplarzy niezależnie ile ajtualnie jest dostępnych książek do wypożyczenia.

![image](https://github.com/user-attachments/assets/7fdd359c-5099-4cd9-b515-ea3c11967272)

## Tabela `books`:  Przechowuje informacje o książkach dostępnych w bazie danych. Zawiera dane takie jak identyfikator książki (ID), tytuł, autora oraz całkowitą liczbę egzemplarzy, niezależnie od tego, ile z nich jest aktualnie dostępnych do wypożyczenia.

![image](https://github.com/user-attachments/assets/7fdd359c-5099-4cd9-b515-ea3c11967272)

## Tabela `rentals`:  Przechowuje informacje o książkach dostępnych w bazie danych. Zawiera dane takie jak identyfikator książki (ID), tytuł, autora oraz całkowitą liczbę egzemplarzy, niezależnie od tego, ile z nich jest aktualnie dostępnych do wypożyczenia.

![image](https://github.com/user-attachments/assets/7fdd359c-5099-4cd9-b515-ea3c11967272)





## Funkcje systemu
System rezerwacji książek w bibliotece umożliwia



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



3.Tabela bazy danych H2
4.
5. Baza danych H2
   
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













