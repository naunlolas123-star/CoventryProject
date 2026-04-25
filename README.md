Logistics Tracking System

## Folder Structure

```
run/
├── db/
│   └── Logistic.db               ← shared database (all scripts point here) -Tair Umurzakov part
├── security/
│   └── DB_displayer.py           ← login gate; browse DB after authentication - Yelkhan Serikov part
├── mqtt/
│   ├── encrypted_publisher.py    ← simulates truck; encrypts & publishes MQTT messages - Adil Ospanov part
│   └── encrypted_subscriber.py  ← decrypts MQTT messages; writes to DB
│   └── secret.key                ← generated automatically on first publisher run
├── dashboard/
│   └── dashboard.py              ← live Tkinter UI; real Astana route; updates map - (dashboard and maps file folders) Didar Bissembay part
└── maps/
    ├── astana_route.html         ← overwritten by dashboard.py each tick
    └── truck_map.html            ← static reference map
```
## How to Run (Windows)

Open a terminal (CMD or PowerShell) inside the `run/` folder.

### Option A — Encrypted MQTT pipeline

**Terminal 1** — start the subscriber first so it is ready to receive:
```
cd mqtt
python encrypted_subscriber.py
```

**Terminal 2** — then run the publisher:
```
cd mqtt
python encrypted_publisher.py
```

**Terminal 3** — inspect the database at any time:
```
cd security
python DB_displayer.py
```

### Option B — Live dashboard

**Terminal 1:**
```
cd dashboard
python dashboard.py
```
Then click **"Open Live Map"** in the UI window — it opens `maps/astana_route.html` in your browser.

**Terminal 2** (optional, to inspect DB while dashboard runs):
```
cd security
python DB_displayer.py
```

## Install Dependencies (run once)

```
pip install paho-mqtt cryptography folium osmnx networkx pillow qrcode
```

## Notes

- Always `cd` into the script's own folder before running it — paths are relative.
- `secret.key` is created automatically inside `mqtt/` when you run the publisher.
- `astana_route.html` in `maps/` is overwritten every 400 ms while the dashboard runs.
- `DB_displayer.py` can be opened in a second terminal at any time without stopping other scripts.
