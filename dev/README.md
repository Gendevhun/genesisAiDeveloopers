# DevMac Guardian

Privát adatokra figyelő, külső függőség nélküli macOS-ellenőrző fejlesztői gépekhez. Ötpercenként képes mérni a túlterhelést, a tárhelyet, a hálózatot, a Safari hibajelentéseit, valamint az Ollama, MLX, Hermes és OpenClaw állapotát. Az előző eredménnyel összevetve azt is jelzi, mely hibák oldódtak meg.

## Biztonsági alapelvek

* A rendszeres futás csak olvas és helyi jelentést készít.
* Nem tölt fel gépnaplót, felhasználói fájlt, tokent vagy jelszót.
* A jelentések `0600`, a jelentésmappa `0700` jogosultságot kap.
* Automatikus törlés, hálózatátállítás és folyamatölés nincs.
* A `repair` csak három, külön engedélyezett LaunchAgent újraindítását tudja; alapból csak előnézet.
* Blokkolt (`U`) folyamatot nem próbál újraindítani, mert előbb a lemezhibát kell kezelni.

## Ellenőrzések

* CPU-terhelés processzormagonként és szabad memória
* belső/külső kötet szabad helye és elérési késleltetése
* DNS és közvetlen internetelérés
* Ollama, MLX, Hermes, OpenClaw launchd- és helyi HTTP-állapota
* Safari 24 órán belüli crash/hang/spin jelentései
* külső lemezre mutató aktív Hermes/OpenClaw futási könyvtárak
* külső Ollama-tár vagy blob-link, ami sérti a belső aktív tár irányelvét
* korábban jittert okozó Kaspersky Secure Connection folyamatok

## Használat

```bash
cd ~/Projects/devmac-guardian
PYTHONPATH=src /usr/bin/python3 -m devmac_guardian check
PYTHONPATH=src /usr/bin/python3 -m devmac_guardian check --output markdown
PYTHONPATH=src /usr/bin/python3 -m devmac_guardian repair
PYTHONPATH=src /usr/bin/python3 -m devmac_guardian repair --apply
```

Az ütemezett, alacsony I/O-prioritású LaunchAgent telepítése:

```bash
PYTHONPATH=src /usr/bin/python3 -m devmac_guardian install
```

Eltávolítás (a jelentések megmaradnak):

```bash
PYTHONPATH=src /usr/bin/python3 -m devmac_guardian uninstall
```

## Helyi fájlok

* konfiguráció: `~/Library/Application Support/DevMacGuardian/config.toml`
* aktuális JSON: `~/Library/Application Support/DevMacGuardian/status.json`
* olvasható jelentés: `~/Library/Application Support/DevMacGuardian/current.md`
* tömör előzmény: `~/Library/Application Support/DevMacGuardian/history.jsonl`
* futási napló: `~/Library/Logs/DevMacGuardian/`

Ezek a fájlok szándékosan nincsenek a GitHub repóban.

## Fejlesztés

```bash
python3 -m venv .venv
.venv/bin/python -m pip install -e '.[test]'
.venv/bin/python -m pytest -q
python tools/policy_check.py
```
