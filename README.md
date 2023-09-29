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

8) Rozdział Ósmy - Wzorce architektoniczne

**Architektura Warstwowa:**
>*Architektura Warstwowa* - w tym wzorcu baza kodu jest zorganizowana w poziome warstwy, przy czym każda warstwa rozwiązuje jeden z następujących problemów technicznych: interakcja z konsumentami, implementacja Logiki Biznesowej i utrwalanie danych. W swojej klasycznej formie Architektura Warstwowa składa się z trzech warstw: Warstwy Prezentacji, Warstwy Logiki Biznesowej i Warstwy Dostępu Do Danych.

>*Warstwa Prezentacji* - implementuje interfejs użytkownika programu do interakcji z jego konsumentami. W oryginalnej formie wzorca warstwa ta oznacza interfejs graficzny, taki jak interfejs webowy lub aplikacja desktopowa.

>*Warstwa Logiki Biznesowej* - warstwa odpowiedzialna za implementację i hermetyzację Logiki Biznesowej programu. Jest to miejsce, w którym są realizowane decyzje biznesowe. W tej warstwie są zaimplementowane wzorce takie jak Aktywny Rekord lub Model Dziedziny.

>*Warstwa Dostępu Do Danych* - warstwa zapewniająca dostęp do mechanizmów utrwalania. W oryginalnej formie wzorca mechanizmem utrwalania była systemowa baza danych.

>*Komunikacja między warstwami* - Warstwy są zintegrowane w modelu komunikacji góra-dół: każda warstwa może utrzymywać zależność tylko od warstwy bezpośrednio pod nią(czyli Warstwa Prezentacji z Warstwą Logiki Biznesowej i vice versa oraz Warstwa Logiki Biznesowej i Warstwa Dostępu Do Danych). Taka architektura wymusza oddzielenie problemów związanych z implementacją i ogranicza zakres wiedzy współdzielonej między warstwami.

*Często zdarza się, że wzorzec Architektury Warstwowej jest rozszerzony o dodatkową warstwę Warstwa Usług*

>*Warstwa Usług* - działa jako pośrednik między prezentacją programu, a Warstawami Logiki Biznesowej. W kontekście wzorca architektonicznego Warstwa Usługi jest granicą logiczną. Nie jest to fizyczna usługa. Warstwa Usług spełnia dla Warstwy Logiki Biznesowej rolę fasady: udostępnia interfejs, który odpowiada metodom interfejsu publicznego oraz hermetyzuje wymaganą orkiestrację bazowych warstw.

**Porty i Adaptery:**
>*Porty i Adaptery* - wzorzec rozwiązujący niedociągnięcia Architektury Warstwowej i lepiej nadaje się do implementacji bardziej złożonej Logiki Biznesowej. Oba wzorce są dość podobne.

>*Warstwa Infrastruktury* - warstwa będąca połączeniem Warstwy Prezentacji i Warstwy Dostępu Do Danych w celu ujednolicenia wszystkich infrastrukturalnych problemów wynikających z nie odzwierciedlania Logiki Biznesowej.

>*Zasada inwersji zależności* - mówi, że moduły wysokiego poziomu, które implementują Logikę Biznesową, nie powinny zależeć od modułów niskiego poziomu. W tym celu odwracamy zależność (funkcjonuje komunikacja dół-góra). Na koniec dodajemy Warstwę Aplikacji jako fasadę dla publicznego interfejsu systemu. Podobnie jak Warstwa Usług w Architekturze Wartwowej, opisuje ona wszystkie operacje udostępniane przez system i organizuje Logikę Biznesową systemu w celu ich wykonania.

>*Integracja komponentów infrastrukturalnych* - Warstwa Logiki Biznesowej, zamiast odwoływać się bezpośrednio do komponentów infrastruktury, definiuje "Porty", które muszą zostać zaimplementowane przez Warstwę Infrastruktury. Warstwa Infrastruktury implementuje z kolei "Adaptery": konkretne implementacje interfejsów Portów do pracy z różnymi technologiami. Abstrakcyjne Porty są implementowane przez konkretne Adaptery w Warstwie Infrastruktury albo przez wstrzykiwanie zależności, albo przez bootstrapping.

**CQRS:**
>*CQRS* - wzorzec Segregacji Odpowiedzialności za Polecenia i Zapytania opiera się na tych samych zasadach organizacyjnych dotyczących Logiki Biznesowej i problemów infrastrukturalnych, co wzorzec Porty i Adaptery. Różni się jednak spospobem zarządzania danymi systemu. Wzorzec CQRS umożliwia reprezentowanie danych systemu w wielu modelach utrwalania.

>*Model Wykonywania Poleceń* wykonuje operacje modyfikujące stan systemu(polecenia systemowe) oraz służy do implementowania Logiki Biznesowej, sprawdzania poprawności reguł i wymuszania niezmienników. Model Wykonywania Poleceń jest również jedynym modelem reprezentującym silnie spójne dane - źródłem prawdy systemu. Model zapewnia możliwość odczytywania silnie spójnego stanu encji biznesowej oraz wykorzystanie wsparcia dla mechanizmu optymistycznej współbieżności podczas aktualizacji stanu. 

>*Model Odczytu (projekcji)* jest zaprogramowaną projekcją. Może być przechowywany w trwałej bazie danych, płaskim pliku lub pamięci podręcznej. właściwa implementacja CQRS pozwala na wymazanie wszystkich danych projekcji i ich odtworzenie od podstaw. Umożliwa to również rozszerzenie systemu o dodatkowe projekcje w przyszłości - modele, których pierwotnie nie można było przewidzieć. Modele Odczytu są tylko do odczytu.

>*Projekcje synchroniczne* - pobierają zmiany w danych OLTP z wykorzystaniem modelu subskrypcji catch-up(dosłownie: doganiania). Silnik projekcji wysyła zapytanie do bazy danych OLTP o dodane lub zaktualizowane rekordy po ostatnim punkcie kontrolnym. Silnik projekcji wykorzystuje zaktualizowane dane do odtworzenia (aktualizacji) Modeli Odczytu systemu. Silnik projekcji przechowuje punkt kontrolny ostatnio przetworzonego rekordu. Ta wartość zostanie użyta w następnej iteracji do uzyskania rekordów dodanych lub zmodyfikowanych po ostatnio przetworzonym rekordzie. Aby subskrypcja catch-up działała, Model Wykonywania Poleceń musi sprawdzić wszystkie dołączone lub zaktualizowane rekordy bazy danych. Mechanizm magazynu danych powinien również obsługiwać kwerendy rekordów na podstawie punktu kontrolnego. Punkt kontrolny można zaimplementować za pomocą mechanizmów bazy danych.

>*Projekcje asynchroniczne* - Model Wykonywania Poleceń publikuje wszystkie zatwierdzone zmiany w magistrali komunikatów. Silniki projekcji systemu mogą subskrybować publikowane wiadomości i używać ich do aktualizacji Modeli Odczytu.

**Kiedy używać Architektury Warstwowej?**
- Zależność między Logiką Biznesową, a Warstwami Dostępu Do Danych sprawia, że ten wzorzec architektury dobrze pasuje do systemu z Logiką Biznesową zaimplementowaną przy użyciu wzorców Skrypt Transakcji lub Aktywny Rekord.

**Kiedy używać Porty i Adaptery?**
- Dzięki oddzieleniu Logiki Biznesowej od wszystkich problemów technologicznych architektura Porty i Adaptery idealnie pasuje do Logiki Biznesowej zaimplementowanej wewnątrz wzorca Modelu Dziedziny.

**Kiedy używać CQRS?**
- We wzorcu CQRS te same dane są reprezentowane w wielu modelach. Chociaż jest on obowiązkowy dla systemów opartych na Modelu Dziedziny ze źródłem w postaci zdarzeń, może być również używany w dowolnych innych systemach, które wymagają pracy z wieloma modelami utrwalania.
