# oswietlenie-adam-kaniowski
Projekt oświetlenia schodów dla Adama Kaniowskiego. 

## Refaktoryzacja kodu wprowadza kilka kluczowych ulepszeń, które warto podkreślić:

Stałe zamiast magicznych liczb: Przeniosłem wartości takie jak liczba LED, jasność czy limity odległości do constexpr. Dzięki temu kod jest bardziej czytelny, łatwiejszy do modyfikacji i mniej podatny na błędy.

Podział na funkcje: Logika obsługi animacji, czujników i aktualizacji świateł została oddzielona. Dzięki temu łatwiej jest zrozumieć, co każda część programu robi, oraz potencjalnie testować każdą funkcję osobno.

Zwiększona odporność na błędy: W funkcji inicjalizacji czujników dodałem mechanizm ponownych prób (retry), aby obsłużyć sytuacje, w których czujnik nie inicjalizuje się poprawnie za pierwszym razem.

Korzystanie z constexpr zamiast #define: Współczesne C++ preferuje constexpr jako bardziej typowo bezpieczną alternatywę dla #define.

Modularność animacji: Logika związana z animacjami jest lepiej oddzielona od pozostałych elementów kodu. Dzięki temu można łatwiej dodawać nowe efekty.

Zmniejszenie BUFFER_SIZE: Zmieniono wielkość bufora z 64 na 8 bajtów, bufor nie jest aktualnie używany w programie. Dzięki temu zwolniono 56 bajtów pamięci.

Dodano bardziej szczegółowe logowanie błędów: Wysyłanie logów do portu szeregowego co 30 sekund i ostrzeżenia przy zapełnianiu się bufora i pamięci RAM, co ułatwi diagnostykę problemów w działającym urządzeniu.


## Uwagi do dalszej optymalizacji:
Pamięć RAM: Arduino Mega 2560 ma ograniczoną pamięć RAM (2 KB???). Obsługa taśmy LED o długości 950 pikseli, szczególnie przy dużej liczbie animacji, może ją mocno obciążać. Warto monitorować użycie pamięci w czasie pracy, szczególnie przy dodawaniu bardziej złożonych efektów.

Segmentacja danych LED: Segmentacja danych LED polega na dzieleniu całego paska diod LED na mniejsze grupy (segmenty), które są obsługiwane sekwencyjnie. Dzięki temu w danym momencie przetwarzana jest tylko część paska, co zmniejsza zapotrzebowanie na pamięć RAM.

Alternatywa dla Mega 2560: Jeśli pojawią się problemy z wydajnością, można rozważyć użycie płytki z mocniejszym procesorem i większą pamięcią, np. ESP32. ESP32 ma nie tylko więcej pamięci, ale także lepsze wsparcie dla wielozadaniowości i obsługi diod LED.

Animacje: Warto przemyśleć sposób implementacji nowych animacji, aby były one definiowane w zunifikowany sposób (np. jako funkcje przechowywane w tablicy wskaźników na funkcje).

Testy długoterminowe: Zalecam przetestowanie kodu pod kątem stabilności w długim czasie, szczególnie przy obciążeniu i intensywnym użytkowaniu.

Podsumowanie
Kod jest obecnie bardziej czytelny i łatwiejszy do utrzymania. Jeśli zależy Ci na skalowalności (np. dodawaniu większej liczby animacji), warto rozważyć przejście na platformę z większymi możliwościami.
