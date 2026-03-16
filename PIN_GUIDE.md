# System kodów PIN / PIN Code System

Ten dokument wyjaśnia przeznaczenie kodów PIN stosowanych w integracji Easy Wallbox.
This document explains the purpose of the PIN codes used in the Easy Wallbox integration.

---

## 1. Kod parowania BLE (Passkey) / BLE Pairing PIN (Passkey)

**Użycie / Usage:**
Jest to standardowy kod parowania Bluetooth (Bonding). Jest wysyłany na żądanie stosu BLE, aby umożliwić bezpieczne połączenie między ESP32 a ładowarką.
This is a standard Bluetooth pairing code (Bonding). It is sent upon request from the BLE stack to establish a secure connection between the ESP32 and the charger.

- **W kodzie / In code:** `ble_client.passkey_reply` -> `7917` (lub `1234`).
- **Skąd wziąć? / Where to get it?**: 
  - Najczęściej jest to kod **7917** lub **1234**.
  - Często jest identyczny z kodem aplikacji.
  - Usually it's **7917** or **1234**. Often identical to the app PIN.

---

## 2. Kod Autoryzacji Protokołu / Protocol Authorization PIN (AUTH)

**Użycie / Usage:**
Jest to kod wysyłany wewnątrz komendy tekstowej `$BLE,AUTH,XXXX`. Bez pomyślnej autoryzacji tym kodem, ładowarka nie będzie odpowiadać na żadne zapytania o dane (`$DATA`) ani polecenia sterujące (`$CMD`).
This is the code sent inside the text command `$BLE,AUTH,XXXX`. Without successful authorization using this code, the charger will not respond to any data queries (`$DATA`) or control commands (`$CMD`).

- **W kodzie / In code:** `$BLE,AUTH,7917` (wysyłane w bloku `on_connect` po 5-8 sekundach).
- **Skąd wziąć? / Where to get it?**:
  - Znajduje się na **naklejce na obudowie ładowarki**.
  - Jest widoczny w oficjalnej aplikacji **eSolution Charging**.
  - Typowe wartości to **7917**, **9844** lub **001234**.
  - Located on a **sticker on the charger's casing**.
  - Visible in the official **eSolution Charging** app.
  - Common values: **7917**, **9844**, or **001234**.

---

## Logika działania / Operational Logic

1. **Połączenie / Connection**: ESP32 łączy się z ładowarką przez BLE.
2. **Parowanie / Pairing**: Jeśli ładowarka tego wymaga, ESP32 wysyła Passkey. Wiele modeli (np. eWB11310) używa trybu "Just Works" i nie wymaga tego PINu.
   *If required, ESP32 sends the Passkey. Many models (e.g., eWB11310) use "Just Works" mode and do not require this PIN.*
3. **Autoryzacja / Authorization**: Po stabilizacji połączenia, ESP32 MUSI wysłać `$BLE,AUTH,[PIN]`.
   *Once connected, ESP32 MUST send `$BLE,AUTH,[PIN]`.*
4. **Praca / Operation**: Po otrzymaniu `$BLE,AUTH,OK` od ładowarki, ESP32 zaczyna cyklicznie odpytywać o dane.
   *After receiving `$BLE,AUTH,OK`, ESP32 begins periodic data polling.*

> [!CAUTION]
> Użycie błędnego kodu AUTH zazwyczaj skutkuje brakiem jakiejkolwiek odpowiedzi (Timeout) lub błędem `$BLE,AUTH,FAIL`.
> *Using the wrong AUTH code usually results in no response (Timeout) or a `$BLE,AUTH,FAIL` error.*
