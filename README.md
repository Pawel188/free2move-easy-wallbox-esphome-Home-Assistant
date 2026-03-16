# Easy Wallbox ESPHome Integration

Integracja ładowarki eSolution Charging Easy Wallbox z Home Assistant przy użyciu ESPHome i BLE.

## Przegląd

Ten projekt pozwala na zdalne monitorowanie i sterowanie ładowarką Easy Wallbox bez konieczności używania oficjalnej aplikacji mobilnej. Cała logika komunikacji BLE została zaimplementowana bezpośrednio w ESPHome, co zapewnia stabilność i szybkość działania.

### Główne Funkcje

- **Monitorowanie Energii**: Odczyt napięcia (V), natężenia (A), mocy (kW) oraz energii sesji (kWh).
- **Sterowanie Ładowaniem**: Przełącznik Start/Stop.
- **Zarządzanie Mocą**: Ustawianie limitów prądu (User Limit i DPM Limit) w kW.
- **Status DPM**: Przełącznik funkcji Dynamic Power Management.
- **Natywna Integracja**: Pełna kompatybilność z Home Assistant przez API ESPHome.

## Instalacja

1. Skopiuj plik `easywallbox-proxy.yaml` oraz `secrets.yaml.example` do swojego folderu ESPHome.
2. Zmień nazwę `secrets.yaml.example` na `secrets.yaml` i uzupełnij swoje dane (WiFi, klucze API).
3. Skompiluj i wgraj oprogramowanie na swoje urządzenie ESP32 (rekomendowany ESP32-S3).
4. Dodaj urządzenie w Home Assistant.

## Dokumentacja

Pełna dokumentacja projektu znajduje się w pliku [DOCS_PLAN.md](./DOCS_PLAN.md) (w trakcie przygotowania).

---
Projekt bazuje na reverse-engineeringu protokołu Bluetooth ładowarki.
