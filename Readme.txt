# ❄️ OSCAR FRIDGE OS - Wersja 1.0

Z dumą prezentuję **OSCAR FRIDGE OS 1.0** – zaawansowany system operacyjny (IoT) stworzony do inteligentnego sterowania układami chłodzenia opartymi na ogniwach Peltiera. 

Projekt wykorzystuje nowoczesną, dwuprocesorową architekturę sprzętową, oddzielając "Mózg" (logika i sieć) od "Mięśni" (sterowanie tranzystorami dużej mocy).

## 🚀 Główne funkcje wydania 1.0

### 🧠 Architektura Dual-MCU
* **Mózg (ESP8266):** Odpowiada za serwer WWW, łączność Wi-Fi, harmonogramy NTP, zaawansowany algorytm PID z predykcją (Predictive Kick) oraz AI Lab.
* **Mięśnie (Arduino Nano):** Odbiera komendy po UART (RX/TX) i steruje tranzystorami MOSFET z użyciem **Ultrasonic PWM (31.25 kHz)**, co gwarantuje absolutną ciszę wentylatorów (całkowita likwidacja buczenia sprzętowego).

### 🌍 Interfejs "Dark Mode HUD" (Web GUI)
* Zaawansowany panel kontrolny dostępny w przeglądarce.
* **Observer:** Na żywo raportujący logi diagnostyczne i decyzje podejmowane przez algorytm.
* **Wykresy Canvas:** Płynne rysowanie krzywych temperatury i map termicznych w czasie rzeczywistym.
* Możliwość sterowania twardymi limitami PWM oraz bezwładnością z poziomu telefonu.

### 🔐 Hardware DRM & Czarna Skrzynka
* **Cyfrowe plomby czujników:** System weryfikuje czujniki DS18B20 na poziomie pamięci SRAM/EEPROM. Zabezpieczenie przed nieautoryzowaną ingerencją w kable.
* **Black Box (EEPROM):** Zapisuje 10 ostatnich krytycznych błędów (np. przegrzanie, brak sygnału z komory, zablokowany wentylator) i przechowuje je nawet po zaniku zasilania.

### 📡 FOTA (Firmware Over-The-Air) & Auto-Recovery
* System samoczynnie (raz na 24h) łączy się z repozytorium GitHub po szyfrowanym protokole HTTPS i weryfikuje wydanie nowych wersji kodu.
* Możliwość bezprzewodowej aktualizacji "w locie" z pobraniem pliku `firmware.bin`.
* **Anti-Freeze Wi-Fi:** Jeśli router domowy ulegnie awarii, lodówka bezpiecznie (bez zjawiska WDT Crash) podniesie własny Hotspot awaryjny (`OSCAR_FRIDGE`) z adresem awaryjnym `192.168.4.1`.

### 🌙 Zaawansowane Zarządzanie Energią (Harmonogramy NTP)
* Zautomatyzowane tryby: **TURBO, IDLE, ECO, SILENT**.
* Wbudowany zegar czasu rzeczywistego (NTP) pozwala wyznaczyć twarde ramy ciszy nocnej (np. od 22:00 do 06:00), maksymalnie ograniczając obroty wentylatora podczas snu.

---

## 🛠️ Jak wykonać aktualizację FOTA?
System jest w pełni bezobsługowy, ale możesz wymusić aktualizację ręcznie:
1. Skompiluj nowy kod w Arduino IDE (`Szkic` -> `Eksportuj skompilowany plik binarzy`).
2. Podmień plik `firmware.bin` w tym repozytorium.
3. Podnieś numerek wersji w pliku `version.txt` (np. z `2.0` na `2.1`).
4. W panelu sterowania lodówki (zakładka System) kliknij: **SPRAWDŹ AKTUALIZACJE Z GITHUB**.
5. Urządzenie samo pobierze oprogramowanie i bezpiecznie uruchomi się ponownie.

---
*Zaprojektowano z inżynieryjną precyzją. Chłodzenie jeszcze nigdy nie było tak inteligentne.*