# Plan Dokumentacji Projektu Easy Wallbox ESPHome

Ten dokument opisuje plan rozwoju dokumentacji dla projektu integracji ładowarki Easy Wallbox.

## 1. Dokumentacja Techniczna (Protokół BLE)
**Cel:** Opisanie sposobu komunikacji z ładowarką dla deweloperów chcących rozbudować projekt.
- Opis UUID serwisów i charakterystyk.
- Lista komend tekstowych (np. `$BLE,AUTH,7917`, `$DATA,READ,SV`).
- Sposób parsowania odpowiedzi (bufferowanie fragmentów, regexy).

## 2. Instrukcja Użytkownika (Hardware)
**Cel:** Pomoc w doborze i przygotowaniu sprzętu.
- Rekomendowane moduły ESP32 (dlaczego S3 jest lepszy ze względu na antenę i RAM).
- Schemat połączenia (zasilanie).
- Wskazówki dotyczące zasięgu BLE w garażu.

## 3. Przewodnik Konfiguracji Home Assistant
**Cel:** Wykorzystanie pełnego potencjału integracji w HA.
- Przykładowa karta Dashboard (Lovelace).
- Automatyzacje (np. ładowanie tylko z fotowoltaiki).
- Integracja z Energy Dashboard.

## 4. Rozwiązywanie Problemów (Troubleshooting)
**Cel:** Samodzielna naprawa najczęstszych błędów.
- Logi ESPHome – jak interpretować błędy AUTH czy timeouty BLE.
- Resetowanie powiązania (bonding) – obsługa usługi `remove_bond_and_reconnect`.
- Problemy z zasięgiem i zakłóceniami WiFi/Bluetooth.

---
**Status:** Planowanie zakończone. Dokumentacja będzie powstawać etapami wraz z rozwojem repozytorium.
