# Lightcap

Lightcap is a Kivy/KivyMD desktop/mobile security scanner that blends lightweight LLM analysis with color-change heuristics and Pennylane-backed entropy signals to classify risk levels. It includes a capture pipeline for Android, a local encrypted history store, and a UI for scanning, model management, playback, and security operations.

## Highlights
- **Hybrid risk engine**: combines LLM output with color-change deltas and a Pennylane-based entropy signal for Low/Medium/High risk classification.
- **Color-change pipeline**: compare movement-alarm vs settle-state color samples, compute deltas, and feed a quantum-inspired circuit for risk biasing.
- **Forecasting**: generates hourly risk outlooks for 47h and 700h based on the color-shift signal.
- **Encrypted persistence**: stores chat and security events in an AES-encrypted SQLite database.
- **Android capture**: supports 24/7 chunked video capture on Android (desktop UI offers status only).

## Project layout
- `main.py`: application logic, UI layout, risk pipeline, model management, and encrypted storage.
- `requirements.txt`: Python dependencies (Kivy, KivyMD, Pennylane, etc.).
- `p4a_recipes/`: build support for Python-for-Android.
- `bulldozer.spec`: Android build configuration.

## Quick start
```bash
python3 -m pip install -r requirements.txt
python3 main.py
```

> Note: Desktop environments may require OpenGL/X11 libraries to launch the Kivy window. Android capture relies on device permissions and hardware support.

## Using the scanner
1. Open the **Scanner** tab.
2. Enter site context (site/zone/human activity/etc.).
3. Provide movement-alarm and settle-state color samples (hex or numeric RGB) to enable the color-change pipeline.
4. Click **Scan Security Risk** to generate a Low/Medium/High label and forecasts.

### Color sample formats
- Hex: `alarm:#FF3366; settle:#112233`
- Numeric: `alarm:120,30,40; settle:10,20,30`
- Multiple labels are supported: `door:#FFAA00; window:#2255FF`

## Security & storage
- The app encrypts its SQLite database and model files using AES.
- Rekey operations are available under the **Security** tab.

## Development notes
- Pennylane is optional at runtime; the app includes deterministic fallbacks if quantum libraries are unavailable.
- The UI is built with KivyMD and custom widgets (risk wheel, gradient buttons, color tab).

## License
See `LICENSE` for details.
