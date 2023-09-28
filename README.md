# Koncepcja_DDD
Moje postępy w nauce z książką Koncepcja Domain-Driven Design Vlada Khononova
1) Rozdział pierwszy - Analiza Dziedzin Biznesowych
> *Poddziedziny Podstawowe* - Innowacje firmy. Działania, które firma wykonuje inaczej niż jej konkurenci i z których czerpie przewagę konkurencyjną.

> *Poddziedziny Ogólne* - Problemy rozwiązane. Są to działania, które wszystkie firmy wykonują w ten sam sposób. Nie ma tu ani miejsca, ani potrzeby innowacji; Zamiast tworzyć wewnętrzne implementacje, bardziej opłacalne jest korzystanie z istniejących rozwiązań.

> *Poddziedziny pomocniczne* - Problemy, dla których istnieją oczywiste rozwiązania. Są to działania, które firma prawdopodobnie będzie musiała zaimplementować wewnętrznie, ale które nie zapewniają jej żadnej przewagi konkurencyjnej.
2) Rozdział drugi - Odkrywanie wiedzy dziedzinowej
> *Język Wszechobecny* jest to narzędzie do wypełniania luki w wiedzy pomiędzy ekspertami dziedzinowymi, a inżynierami oprogramowania. Aby zapewnić skuteczną komunikację, z Języka Wszechobecnego trzeba wyeliminować niejasność i ukryte założenia. Wszystkie terminy języka powinny być spójne, nie powinny zawierać terminów niejednoznacznych ani synonimów.
3) Rozdział trzeci - Zarządzanie złożonością Dziedziny
> *Konteksty ograniczone* dekomponują system na komponenty fizyczne - usługi, podsystemy itd. W różnych kontekstach ograniczonych te same terminy mogą mieć różne znaczenia np. słowo "Lead", w kontekście marketingu znaczy Zdarzenie, a w kontekście sprzedaży Złożony podmiot. Konteksty ograniczone muszą ze sobą współpracować, aby utworzyć system.
4) Rozdział Czwarty - Integracja Kontekstów Ograniczonych

**Wzorce definiujące integracje Kontekstów Ograniczonych:**

> *Partnerstwo* - Konteksty Ograniczone są integrowane w sposób doraźny.

> *Wspólne Jądro* - Dwa lub więcej Kontekstów Ograniczonych jest zintegrowanych przez współdzielenie ograniczonego, nakładającego się modelu, należącego do wszystkich korzystających z tego modelu Kontekstów Ograniczonych.

> *Konformista* - Konsument dostosowuje się do modelu usługodawcy.

> *Warstwa Antykorupcyjna* - Konsument tłumaczy model usługodawcy na model odpowiadający potrzebom konsumenta.

> *Usługa Otwartego Hosta* - Usługodawca implementuje Język Opublikowany - model zoptymalizowany pod kątem potrzeb konsumentów.

> *Różne Drogi* - Powielanie określonych funkcji jest tańsze niż współpraca i integracja.
5) Rozdział Piąty - Implementacja prostej Logiki Biznesowej

**Wzorce implementacji Logiki Biznesowej:**
>*Skrypt Transakcji* - Ten wzorzec organizuje operacje systemu jako proste skrypty proceduralne. Procedury są skonstruowane w taki sposób, aby każda operacja miała charakter transakcyjny - albo się powiedzie, albo nie. Wzorzec Skrypt Transakcji nadaje się do obsługi Poddziedzin, z Logiką Biznesową przypominającą proste operacje ETL.

>*Aktywny Rekord* - Gdy Logika Biznesowa jest prosta, ale działa na skomplikowanych strukturach danych, można zaimplementować te struktury danych jako Aktywne Rekordy. Aktywny Rekord to struktura danych, która zapewnia proste metody dostępu do danych CRUD.
6) Rozdział Szósty - Rozwiązywanie problemów ze złożoną Logiką Biznesową

**Wzorzec Modelu Dziedziny składa się z:**
>*Obiekty Wartości* - Pojęcia Dziedziny Biznesowej, które można zidentyfikować wyłącznie na podstawie ich wartości, a w związku z tym nie wymagają wyraźnego pola identyfikatora. Ponieważ zmiana w jednym z pól semantycznie tworzy nową wartość, Obiekty Wartości są niezmienne.
Obiekty Wartości modelują nie tylko dane, ale także zachowanie: metody manipulujące wartościami, a tym samym inicjujące nowe Obiekty Wartości.

>*Agregaty* - Hierarchia encji współużytkujących granicę transakcji. Aby można było zaimplementować Logikę Biznesową Agregatu, wszystkie dane zawarte w jego granicach muszą być silnie spójne.
Stan Agregatu i jego wewnętrznych obiektów można modyfikować tylko za pośrednictwem publicznego interfejsu, poprzez wykonywanie poleceń. Pola danych dla komponentów zewnętrznych są tylko do odczytu, dzięki czemu cała Logika Biznesowa związana z Agregatem znajduje się w jego granicach.
Agregat spełnia rolę granicy transakcji. Wszystkie jego dane, w tym wszystkie jego wewnętrzne obiekty, muszą być włączone do bazy danych jako jedna atomowa transakcja. Agregat może komunikować się z encjami zewnętrznymi poprzez publikowanie Zdarzeń Dziedziny - komunikatów opisujących ważne zdarzenia biznesowe w cyklu życia Agregatu. Inne komponenty moga subskrybować zdarzenia i używać ich do inicjowania wykonywania Logiki Biznesowej.

>*Usługi Dziedziny* - Obiekty bezstanowe obsługujące Logikę Biznesową, która naturalnie nie należy do żadnego Agregatu, ani Obiektów Wartości Modelu Dziedziny.

7) Rozdział Siódmy - Modelowanie wymiaru czasu
>*Event Sourcing* - to podejście do projektowania i modelowania systemów informatycznych, w którym stan systemu jest reprezentowany jako sekwencja zdarzeń (eventów). Zamiast przechowywać tylko bieżący stan systemu, event sourcing gromadzi wszystkie zdarzenia, które wystąpiły w systemie w czasie. Te zdarzenia są trwałe i niezmienne, co oznacza, że raz dodane do systemu nie mogą być zmieniane ani usuwane.
