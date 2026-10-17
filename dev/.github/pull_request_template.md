# pull\_request\_template

### Eredmény

### Biztonság és adatvédelem

* [ ] Nem kerül titok, helyi jelentés vagy felhasználói adat a diffbe.
* [ ] A rendszeres ellenőrzés továbbra is csak olvasható.
* [ ] Új javítási művelet előnézetes, engedélylistás és nem töröl adatot.

### Bizonyíték

* [ ] `PYTHONPATH=src python3 -m pytest -q`
* [ ] `python3 tools/policy_check.py`
* [ ] `PYTHONPATH=src python3 -m compileall -q src tests tools`

### Visszaállítás
